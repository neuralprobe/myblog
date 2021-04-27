---
layout: page
description: >
  Post listing by categories 
hide_description: true
---
<div class="categories-expo">
  <div class="categories-expo-list">
    {% for cat in site.categories %}
    <a href="#{{ cat[0] | slugify }}" class="post-category">{{ cat[0] | capitalize }}</a>&nbsp;&nbsp;||&nbsp;&nbsp;
    {% endfor %}
  </div>
  <hr />
  <div class="categories-expo-section">
    {% for cat in site.categories %}
    <h2 id="{{ cat[0] | slugify }}">{{ cat | first | capitalize }}</h2>
    <ul class="categoriess-expo-posts">
      {% for post in cat[1] %}
      <a class="post-title" href="{{ site.baseurl }}{{ post.url }}">
        <li>
          {{ post.title }}
          <!-- <small class="post-date">{{ post.date | date_to_string }}</small> -->
        </li>
      </a>
      {% endfor %}
    </ul>
    {% endfor %}
  </div>
</div>
