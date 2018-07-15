---
layout: single
classes: wide
author_profile: true
permalink: /research/
---
{% assign collection = site.research | group_by: "year" %}
<h3 style="text-align:center">Select Publication Year</h3>
<div class="d-flex justify-content-center">
	{% for group in collection reversed%}
		<div class="p-2" style="margin: 0 5px">
			<a href="{{ group.name | prepend: "#y"}}" class="btn btn--primary" type="button"> {{ group.name }} </a>
		</div>
	{% endfor %}
</div>

{% for group in collection reversed %}
<h2 id="{{ group.name | prepend: "y"}}"> {{ group.name }} </h2>
{% for item in group.items reversed %}
<div class="row">
	<div class="col-md-10">
		<h3>{{ item.title }}</h3> 
		<p> {{ item.content }} </p>
	</div>
	<div class="col-md-2">
		<button class="btn btn--primary pdfButton" type="button"  data-toggle="collapse" data-target="#{{ item.collapseID }}" aria-expanded="false" aria-controls="{{ item.collapseID }}"> 
			View PDF
		</button>	
	</div>
</div>

___

<div class="row">
	<div class="collapse" id="{{ item.collapseID }}" style="width:100%">
		<object data="{{ item.pdfUrl }}" type="application/pdf" width="100%" height="100%">
			<p><b>Browser Cannot View PDF</b> <a href="{{ item.pdfUrl }}">Download PDF</a>.</p>
		</object>
	</div>
</div>
{% endfor %}
{% endfor %}