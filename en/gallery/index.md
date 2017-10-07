---
title: Gallery
lang: en
layout: home
stylesheets: lightbox.min
scripts: lightbox.min
---
Here are some photos of microDRUM made by me or members of the forum:

{% assign str_dir = '' %}
{% for file in site.static_files %}
    {% if file.path contains "/gallery/" %}
        {% assign str_tmp = file.path | remove: "/gallery/" %}
        {% if str_dir != '' %}
            {% assign str_dir = str_dir | append: "::" | append: str_tmp %}
        {% else %}
            {% assign str_dir = str_tmp %}
        {% endif %}
    {% endif %}
{% endfor %}
{% assign image_paths = str_dir | split: "::" %}

{% assign str_dir = '' %}
{% assign is_preview = false %}
{% for img_path in image_paths %}
    {% assign arr = img_path | split: '/' %}
    {% if str_dir != arr.first %}
        {% assign is_preview = true %}
        {% assign str_dir = arr.first %}
<h3>{{ str_dir }}</h3>
<div class="album">
    <a href="/gallery/{{ img_path }}" data-lightbox="{{ str_dir }}">
        <img src="/gallery/{{ img_path }}" alt="[{{ str_dir }} image]" style="background-color:white;width:30%;padding:4px;border:1px solid black;margin:4px">
    </a>
</div>
    {% endif %}
    {% if is_preview %}
        {% assign is_preview = false %}
    {% else %}
<a href="/gallery/{{ img_path }}" data-lightbox="{{ str_dir }}"></a>
    {% endif %}
{% endfor %}
