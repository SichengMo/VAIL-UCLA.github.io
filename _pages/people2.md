---
layout: page
permalink: /team/
title: Team
nav: true
nav_order: 5
---


<section class="our-webcoderskull">
<div class="container-fluid">
  {% assign role_groups = site.data.team | group_by: 'role' %}
  {% assign total_groups = role_groups.size %}
  {% assign current_group = 0 %}
  {% assign alumni_groups = '' %}
  {% assign alumni_count = 0 %}
  
  {% for group in role_groups %}
    {% unless group.name contains 'Alumni' %}
      {% assign current_group = current_group | plus: 1 %}
      <h3 class="text-left mb-1">{{ group.name }}</h3>
      {% if current_group < total_groups %}
        <ul class="row mb-0" style="margin-bottom: 0.5rem !important;">
      {% else %}
        <ul class="row" style="margin-bottom: 0 !important;">
      {% endif %}
        {% for member in group.items %}
          <li class="col-12 col-md-4 col-md-2 mb-0">
                <div class="cnt-block equal-hight">
                    <a href="{{ member.link }}" target="_blank">
                              <figure><img src="{{ member.image }}" class="img-responsive" alt="{{ member.name }}" /></figure>
                    </a>
                    <div style="text-align: center;">
                        <h6><a href="{{ member.link }}" target="_blank" style="text-decoration: none;">{{ member.name }}</a></h6>
                    </div>
                    {% unless member.affiliation == "UCLA" %}
                    <small>{{ member.affiliation }}</small>
                    {% endunless %}
                </div>
          </li>
        {% endfor %}
      </ul>
    {% endunless %}
  {% endfor %}
  
  {% comment %} Handle Alumni section separately with subsections {% endcomment %}
  {% assign alumni_groups = '' %}
  {% for group in role_groups %}
    {% if group.name contains 'Alumni' %}
      {% assign alumni_groups = alumni_groups | append: group.name | append: ',' %}
    {% endif %}
  {% endfor %}
  
  {% if alumni_groups != '' %}
    <h3 class="text-left mb-1">Alumni</h3>
    {% assign alumni_array = alumni_groups | split: ',' %}
    {% for alumni_group_name in alumni_array %}
      {% if alumni_group_name != '' %}
        {% for group in role_groups %}
          {% if group.name == alumni_group_name %}
            <h5 class="text-left mb-2" style="color: #666; font-size: 1.3em; margin-top: 1.5rem;">{{ group.name | replace: 'Alumni - ', '' }}</h5>
            <div class="row" style="font-size: 1.1em; margin-bottom: 1.5rem;">
              {% for member in group.items %}
                <div class="col-md-3 col-sm-6 mb-3">
                  <div style="padding: 0.5rem 0.8rem; background-color: #f8f9fa; border-radius: 0.4rem; font-size: 1em; height: 100%; text-align: center;">
                    <a href="{{ member.link }}" target="_blank" style="text-decoration: none; color: #333; font-weight: 500;">{{ member.name }}</a>
                    {% if member.year %}
                    <br><span style="color: #888; font-size: 0.8em; font-style: italic;">{{ member.year }}</span>
                    {% endif %}
                    {% unless member.affiliation == "UCLA" %}
                    <br><span style="color: #666; font-size: 0.85em;">{{ member.affiliation }}</span>
                    {% endunless %}
                  </div>
                </div>
              {% endfor %}
            </div>
          {% endif %}
        {% endfor %}
      {% endif %}
    {% endfor %}
  {% endif %}
</div>
</section>