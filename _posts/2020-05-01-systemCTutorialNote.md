---
layout: post
title: SystemC Tutorial Note
description: >
  Hardware simultion
categories: [scitech]
tags: [hardware, notebook]
image:
  path:  /assets/notes/note_systemCTutorial/firSystem.png
  srcset:
    500w:  /assets/notes/note_systemCTutorial/firSystem_500.png
    1000w:  /assets/notes/note_systemCTutorial/firSystem_1000.png
    1500w:  /assets/notes/note_systemCTutorial/firSystem_1500.png
---


- Table of Contents
{:toc .large-only}

+ source: [Learn SystemC from Forte](https://youtu.be/NCFxBGLB5xs)

## Introduction

+ systemC?
    * library of C++ classes
    * hardware aware
        - concurrency
        - bit accuracy
        - simulation time advancement

    ```cpp
    #include <systemc.h>
    SC_MODULE( and2 ){
        sc_in<DT> a;
        sc_in<DT> b;
        sc_out<DT> f;
        sc_in<bool> clk;
        //DT -> sc_uint<1>

        void func(){
            f.write( a.read() & b.read() );
        }

        SC_CTOR( and2 ){ //systemC constructor  
            //case1
            SC_METHOD(func);
            sensitivity << a << b;

            //case2
            SC_METHOD(func);
            sensitive << clk.pos(); // or clk.neg()
        }
    }
    ```

+ Threads
    * a function made to act like a hardware process
        - run concurrently
        - sensitive to signals, clock edges or fixed amount of simulation time
        - Not called by the user, always active
    * three types
        - SC_METHOD()
            + Executes once every sensitivity event
            + runs continuously
            + verilog's @always block
            + synthesizable
                * useful for combinational expressions or simple sequential logic  
        - SC_THREAD()
            + runs once at start of simulation, then suspends itself when done
            + can contain an infinite loop to execute code at a fixed rate of time
            + similar to @initial block
            + NOT synthesizable
                * uesful for testbenches to describe clocks or initial startup signal sequences  
        - SC_CTHREAD()
            + "clocked thread"
            + runs continuously
            + references a clock edge
            + synthesizable
            + can take one or more clock cycles to execute a single iteration
            + used in 99% of all high-level behavioral designs  
        
+ Integer datatypes:
    * bit-accurate
        - fixed width
        - always 32bits
    * Unsigned and signed
        - sc_uint<N> where N is the bitwidth
        - sc_int<N>


## Using SC_CTHREADs  
+ SC_METHODs
    * Limited to one cycle
    * fine for counters or simple sequential designs
    * not much different than hand coded RTL
    * can't handle multi-cycle algorithms
+ SC_CTHREADs
    * not limted to one cycle
    * can contain continous loops
    * can contain large blocks of code with operations or control 
    * great for behavior synthesis

+ FIR Filter
    * `fir.h`: module and thread declaration  
    ``` cpp
    #include <systemc.h>
    SC_MODULE( fir ){
        sc_in< bool > clk;
        sc_in< bool > rst;
        sc_in< sc_int<16> > inp;
        sc_out< sc_int<16> > outp;

        void fir_main(); //just declaration here

        SC_CTOR( fir ){ //systemC constructor  
            SC_CTHREAD( fir_main, clk.pos() );
            reset_signal_is(rst, true );
        }
    }

    // Coefficients for each FIR
    const sc_unint<8> coef[5] = {18,77,107,77,18};
    ```
    * `fir.cc`: thread definition  

    ```cpp
    // FIR Main thread
    #include "fir.h"

    void fir::fir_main(void)
    {
        // Reset code
        // Reset internal variables
        // Reset outputs
        sc_int<16> taps[5]; // set coefficients
        outp.write( 0 ); // initialize
        wait();

        while( true ){
            // Read inputs
            // Algorithm code
            // Write outputs

            for(int i = 4; i > 0; i--){
                taps[i] = taps[i-1];
            }
            taps[0]=inp.read();

            sc_int<16> val;
            for(int i=0; i < 5; i++){
                val += coef[i]*taps[i];
            }
            outp.write(val);
            wait(); // Associated with 'clk' class
        }
    }
    ```

## Testbenches  
+ Verification
    * Hierarchical test environment
        - top level test structure
            + instance of FIR module (DUT)
            + instance of testbench module
            + connectivity
        - tentbench module

![image](/assets/notes/note_systemCTutorial/firSystem.png)

+ Test environment
    * In a host module `System`
        - Module `fir0` 
            + clk, rst, inp, outp
        - Testbench `tb0` 
            + clk, rst, inp, outp
        - `clk` is generated from systemC

+ Basic `SYSTEM` structure    
    ```cpp
    SC_MODULE( SYSTEM ){
        // Module declarations

        // Local signal declarations

        SC_CTOR( SYSTEM ){ // Constructor
            // Module instance signal connections
        }

        ~SYSTEM()
        // Destructor
    }

    ```
+ `main.cc`
    ```cpp
    #include <systemc.h>
    #include "fir.h"
    #include "tb.h"

    SC_MODULE( SYSTEM ){
        tb *tb0; // declare a pointer(*) to its reference name(tb0)
        fir *fir0;

        sc_signal<bool>         rst_sig;
        sc_signal<sc_int<16>>   inp_sig;
        sc_signal<sc_int<16>>   outp_sig;

        sc_clock clk_sig;

        SC_CTOR( SYSTEM )
            : clk_sig ("clk_sig",10, SC_NS)
        {
            tb0 =  new tb("tb0");
            tb0->clk( clk_sig ); // remind that tb0 is a pointer
            tb0->rst( rst_sig );
            tb0->inp( inp_sig );
            tb0->outp( outp_sig);

            fir0 = new fir("fir0");
            fir0->clk(clk_sig);
            fir0->rst( rst_sig );
            fir0->inp( inp_sig );
            fir0->outp( outp_sig);
        }

        ~SYSTEM(){
            delete tb0;
            delete fir0;
        }
    }

    // SYSTEM instantiation
    SYSTEM *top = NULL;

    int sc_main(int argc, char* argv[]){ 
        // acgc = arg count, argv = arg vector
        top = new SYSTEM("top");
        sc_start();
        return 0;
    }

    ```

+ `tb.h`
    ```cpp
    #include <systemc.h>
    SC_MODULE( tb ){
        sc_in< bool > clk;
        sc_out< bool > rst;       //opposit to fir module
        sc_out< sc_int<16> > inp; //opposit to fir module
        sc_in< sc_int<16> > outp; //opposit to fir module

        void source();
        void sink();

        SC_CTOR(tb){
            SC_CTHREAD( source, clk.pos() );
            SC_CTHREAD( sink, clk.pos() );
        }

    ```

+ `tb.cc`
    ```cpp
    #include "tb.h"

    void tb::source(){
        //reset
        inp.write( 0 );
        rst.write( 1 );
        wait();
        rst.write( 0 );
        wait();


        sc_int<16> tmp;
        //send stimulus to FIR
        for( int i=0; i<64; i++){
            if(i>23 && i<29)
                tmp = 256;
            else
                tmp = 0;
            inp.write( tmp );
            wait();
        }
    }

    void tb::sink(){
        sc_int<16> indata;
        //Read output coming from DUT
        for(int i = 0; i<64; i++){
            indata = outp.read();
            wait();
            cout << i << " :\t" << indata.to_int() << endl;
        }

        // End simulation
        sc_stop(); // calls destructors
    }

    ```

## Handshaking  

+ In the folder ...
    * `Makefile` file and type `make`  
    * `golden` folder

![image2](/assets/notes/note_systemCTutorial/firSystem2.png)
+ If simulation fails... communication between `tb0` and `fir0` failed
    * Handshake: Add single bit (`bool`) valid(`vld`) and ready(`rdy`) signals for both input/ouput like .. 
    * ![image2](/assets/notes/note_systemCTutorial/firSystem3.png)

    ```cpp
        // Add below to SC_MODULE( SYSTEM )

        sc_signal<bool>         inp_sig_vld;
        sc_signal<bool>         inp_sig_rdy;
        
        sc_signal<bool>         outp_sig_vld;
        sc_signal<bool>         outp_sig_rdy;

        // Add to signal connection in constructor
        // Add valid/ready pins to 'tb.h' and 'fir.h' 
    ```
+ Modeling asynchronous communication at different levels of abstraction using systemC [LINK](http://www.imm.dtu.dk/SoC-Mobinet/material/doc/note-async-systemc-channels.pdf)

















