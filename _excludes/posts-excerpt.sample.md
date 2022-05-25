---
layout: default
nav_item: true
nav_order: 2
title: BLOG
---

<div class="wrapper">
  <div class="content">
    {%- if site.posts.size > 0 -%}
    <ul class="post-list">
      <!-- Uncoment code below, uncoment _config.yml, and include paginator.html to use paginator -->
      <!-- for post in paginator.posts -->
      {%- for post in site.posts -%}
      {%- if post.hide_post != true -%}
      {%- capture first_img_url -%}
      {% include image_set.html content = post.content %}
      {%- endcapture -%}
      {% assign first_img_url = first_img_url | strip %}
      {% if first_img_url.size == 0 or post.show_excerpt_image == false %}
      {% assign show_except_image = "no-image" %}
      {% else %}
      {% assign show_except_image = "with-image" %}
      {% endif %}
      <li class="list-item">
        <div class="list-item-wrapper">
          <div class="list-item-meta {{show_except_image}}">
            {%- assign date_format = site.data_formats.date_format | default: "%b %-d, %Y" -%}
            <p class="item-date">
              {{ post.date | date: date_format }}</p>
            
            <a class="item-link" href="{{ post.url | relative_url }}" target="_blank">
              {{ post.title | escape }}
            </a>
            
            <p class="item-excerpt">
              {{ post.content | strip_html | slice: 0, 200 | strip }}</p>
          </div>
          {% if show_except_image == "with-image" %}
          <a href="{{ post.url | relative_url }}" class="list-item-image"
            style="display: inline-block; width: 100px; height: 100px;">
            <img style="height: 100px; line-height: 130px;border-radius: 17px; object-fit:cover;"
              src="{{first_img_url}}" alt="{{post.title}}" loading="lazy">
          </a>
          {% endif %}
        </div>
      </li>
      {%- endif -%}
      {%- endfor -%}
    </ul>
    {%- endif -%}
    <!-- include pagination.html  -->

    {% include scroll_to_top.html %}
  </div>

</div>