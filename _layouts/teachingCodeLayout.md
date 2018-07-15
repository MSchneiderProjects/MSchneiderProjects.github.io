---
layout: single
---

<div class="row">
	{% for item in page.resources %}
	<div class="col-md" align="center">
		<a class="btn btn--primary" type="button" style="min-width:100px" data-toggle="collapse" href="#{{ item.id }}" aria-expanded="false" aria-controls="{{ item.id }}">
			{{ item.title }}
		</a>
	</div>
    {% endfor %}
</div>
<div id="accordion">
    {% for item in page.resources %}
		{% if item.type == "pdf" %}
			<div class="collapse" id="{{ item.id }}" data-parent="#accordion">
				<object data="{{ item.url }}" type="application/pdf" width="100%" height="100%">
					<p><b>Example fallback content</b>: This browser does not support PDFs. Please download the PDF to view it: <a href="{{ item.url }}">Download PDF</a>.</p>
				</object>
			</div>
		{% elsif item.type == "code" %}
			<div class="collapse" id="{{ item.id }}" data-parent="#accordion">
				{% include_relative {{ item.url }} %}
			</div>
		{% elsif item.type == "video" %}
			<div class="collapse" id="{{ item.id }}" data-parent="#accordion">
				<iframe width=500 height=250 src="https://www.youtube.com/embed/{{ item.url }}" frameborder="0" allowfullscreen></iframe>
			</div>
		{% endif %}
    {% endfor %}
</div>