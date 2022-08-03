---
layout: page
title: Software Tools
description: >
  describe here
hide_description: true
---

- Table of Contents
{:toc .large-only}

## Google Cloud Platform
- 구글 클라우드 설명 [video](https://youtu.be/d4mz9YIf6Gc) [blog](https://kim6394.tistory.com/98) [blog1](https://mc.ai/gcp-vm%EC%97%90%EC%84%9C-nvidia-gpu%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%B4%EB%B3%B4%EC%9E%90/) [sungkim](https://www.youtube.com/watch?v=8Jkz2HexDAM)
- GCP scp [link](https://cloud.google.com/compute/docs/instances/transfer-files?hl=ko#scp)

        > scp -i ~/.ssh/my-ssh-key [LOCAL_FILE_PATH] [USERNAME]@[IP_ADDRESS]:~
 
        > scp -i ~/.ssh/my-ssh-key [USERNAME]@[IP_ADDRESS]:[REMOTE_FILE_PATH] [LOCAL_FILE_PATH]

- My GCP External IP

        > jhshin1026@34.73.225.168:~/

- 로컬에서 Jupyter Notebook 쓰기 [link](https://shwksl101.github.io/gcp/2018/12/23/gcp_vm_custom_setting.html)

        >> IP:1.1.1.1 & Port:8888

        > jupyter-notebook --no-browser --port=8888

        > 로컬 Browser에 34.73.225.168:8888 실행 

## powerstat(ubuntu app)
- [powerstat](http://manpages.ubuntu.com/manpages/xenial/man8/powerstat.8.html): power measurement tool for Ubuntu
- command : 

'''
sudo powerstat -R -c -z > dump.txt
'''

Actual usages in the literature

- reference:

[ASTESJ example](https://www.astesj.com/publications/ASTESJ_020131.pdf)

[IEEE example](https://ieeexplore.ieee.org/abstract/document/7034863)
