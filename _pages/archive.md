---
title: "Blog Archive"
permalink: /archive/
layout: archive
author_profile: true
---

<h2 style="text-align:center">Organize Posts By</h2>
<div class="d-flex justify-content-center">
	<div class="p-2" style="margin: 0 5px">
		<button class="btn btn--primary" type="button"  data-toggle="collapse" data-target="#tags" aria-expanded="false" aria-controls="tags"> 
			Tag
		</button>
	</div>
	<div class="p-2" style="margin: 0 5px">
		<button class="btn btn--primary" type="button"  data-toggle="collapse" data-target="#category" aria-expanded="false" aria-controls="category"> 
			Category
		</button>
	</div>
	<div class="p-2" style="margin: 0 5px">
		<button class="btn btn--primary" type="button"  data-toggle="collapse" data-target="#date" aria-expanded="false" aria-controls="date"> 
			Date
		</button>
	</div>
</div>

<div id="accordion">
<div class="collapse" id="tags" data-parent="#accordion">
{% assign tags_max = 0 %}
{% for tag in site.tags %}
  {% if tag[1].size > tags_max %}
    {% assign tags_max = tag[1].size %}
  {% endif %}
{% endfor %}

<ul class="taxonomy__index">
  {% for i in (1..tags_max) reversed %}
    {% for tag in site.tags %}
      {% if tag[1].size == i %}
        <li>
          <a href="#{{ tag[0] | slugify }}">
            <strong>{{ tag[0] }}</strong> <span class="taxonomy__count">{{ i }}</span>
          </a>
        </li>
      {% endif %}
    {% endfor %}
  {% endfor %}
</ul>

{% for i in (1..tags_max) reversed %}
  {% for tag in site.tags %}
    {% if tag[1].size == i %}
      <section id="{{ tag[0] | slugify | downcase }}" class="taxonomy__section">
        <h2 class="archive__subtitle">{{ tag[0] }}</h2>
        <div class="entries-{{ page.entries_layout | default: 'list' }}">
          {% for post in tag.last %}
            {% include archive-single.html type=page.entries_layout %}
          {% endfor %}
        </div>
        <a href="#page-title" class="back-to-top">{{ site.data.ui-text[site.locale].back_to_top | default: 'Back to Top' }} &uarr;</a>
      </section>
    {% endif %}
  {% endfor %}
{% endfor %}
</div> <!-- End Tags Section -->
<div class="collapse" id="category" data-parent="#accordion">
{% assign categories_max = 0 %}
{% for category in site.categories %}
  {% if category[1].size > categories_max %}
    {% assign categories_max = category[1].size %}
  {% endif %}
{% endfor %}

<ul class="taxonomy__index">
  {% for i in (1..categories_max) reversed %}
    {% for category in site.categories %}
      {% if category[1].size == i %}
        <li>
          <a href="#{{ category[0] | slugify }}">
            <strong>{{ category[0] }}</strong> <span class="taxonomy__count">{{ i }}</span>
          </a>
        </li>
      {% endif %}
    {% endfor %}
  {% endfor %}
</ul>

{% for i in (1..categories_max) reversed %}
  {% for category in site.categories %}
    {% if category[1].size == i %}
      <section id="{{ category[0] | slugify | downcase }}" class="taxonomy__section">
        <h2 class="archive__subtitle">{{ category[0] }}</h2>
        <div class="entries-{{ page.entries_layout | default: 'list' }}">
          {% for post in category.last %}
            {% include archive-single.html type=page.entries_layout %}
          {% endfor %}
        </div>
        <a href="#page-title" class="back-to-top">{{ site.data.ui-text[site.locale].back_to_top | default: 'Back to Top' }} &uarr;</a>
      </section>
    {% endif %}
  {% endfor %}
{% endfor %}

</div><!-- End Category Section -->
<div class="collapse" id="date" data-parent="#accordion">
<ul class="taxonomy__index">
  {% assign postsInYear = site.posts | group_by_exp: 'post', 'post.date | date: "%Y"' %}
  {% for year in postsInYear %}
    <li>
      <a href="#{{ year.name }}">
        <strong>{{ year.name }}</strong> <span class="taxonomy__count">{{ year.items | size }}</span>
      </a>
    </li>
  {% endfor %}
</ul>

{% assign postsByYear = site.posts | group_by_exp: 'post', 'post.date | date: "%Y"' %}
{% for year in postsByYear %}
  <section id="{{ year.name }}" class="taxonomy__section">
    <h2 class="archive__subtitle">{{ year.name }}</h2>
    <div class="entries-{{ page.entries_layout | default: 'list' }}">
      {% for post in year.items %}
        {% include archive-single.html type=page.entries_layout %}
      {% endfor %}
    </div>
    <a href="#page-title" class="back-to-top">{{ site.data.ui-text[site.locale].back_to_top | default: 'Back to Top' }} &uarr;</a>
  </section>
{% endfor %}
</div> <!-- End Date Section -->

</div><!-- End Accordion Collapse -->