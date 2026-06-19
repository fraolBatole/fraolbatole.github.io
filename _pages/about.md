---
layout: about
title: about
permalink: /
subtitle: Engineering Trustworthy AI Systems with program analysis.

profile:
  align: right
  image: profile.jpg
  image_circular: true # crops the image to make it circular
  more_info: >
    <p>New Orleans, Louisiana</p>

news: true # includes a list of news items
selected_papers: true # includes a list of papers marked as "selected={true}"
social: true # includes social icons at the bottom of the page
---

Bio: I am a Ph.D. student in Computer Science at Tulane University, where I recently transitioned with my advisor [Prof. Hridesh Rajan](https://hridesh.github.io/). Prior to joining Tulane, I completed my Master's degree at Iowa State University (ISU) and undertook graduate-level coursework at the University of North Dakota (UND). My academic journey began at Addis Ababa Science and Technology University, where I earned my undergraduate degree in Software Engineering, graduating Magna cum laude.

I am fortunate to collaborate with [Prof. Tien N. Nguyen](https://personal.utdallas.edu/~tien.n.nguyen/), [Prof. Danny Dig](https://danny.cs.colorado.edu/), and [Prof. Foutse Khomh](https://www.khomh.net/).

<hr class="section-sep" />

## Research

My research addresses the engineering of **trustworthy AI systems**. As LLM-based agents take on substantive software engineering tasks, fluent output is not a sufficient measure of correctness. My work builds the mechanisms that make AI behavior verifiable, drawing on program analysis and runtime verification to provide explicit guarantees rather than relying on model confidence alone. Two complementary threads organize this work.

<div class="research-cards row row-cols-1 row-cols-md-2">
  <div class="col">
    <div class="research-card">
      <h3 class="research-card-title">Trustworthy AI Agents</h3>
      <p class="area-desc">Agents whose reasoning is grounded in program analysis and whose actions are verified before they touch a codebase.</p>
      <ul class="fa-papers">
        {% assign agent_papers = site.projects | where: "category", "Trustworthy AI Agents for Code" | where: "first_author", true | sort: "importance" %}
        {% for project in agent_papers %}
          <li class="fa-paper">
            <div class="fa-paper-head">
              <span class="paper-name">{{ project.title }}</span>
              {% if project.venue %}<span class="proj-chip">{{ project.venue }}</span>{% endif %}
            </div>
            <p class="paper-idea">{{ project.description }}</p>
            <a class="read-more" href="{{ project.url | relative_url }}">Read more &rarr;</a>
          </li>
        {% endfor %}
      </ul>
    </div>
  </div>
  <div class="col">
    <div class="research-card">
      <h3 class="research-card-title">Reliable &amp; Verifiable AI</h3>
      <p class="area-desc">Analyzing, verifying, and repairing the AI systems themselves, so their behavior can be trusted and maintained.</p>
      <ul class="fa-papers">
        {% assign reliability_papers = site.projects | where: "category", "Reliable & Verifiable AI" | sort: "importance" %}
        {% for project in reliability_papers %}
          {% if project.first_author or project.title == "IRepair" %}
            <li class="fa-paper">
              <div class="fa-paper-head">
                <span class="paper-name">{{ project.title }}</span>
                {% if project.venue %}<span class="proj-chip">{{ project.venue }}</span>{% endif %}
              </div>
              <p class="paper-idea">{{ project.description }}</p>
              <a class="read-more" href="{{ project.url | relative_url }}">Read more &rarr;</a>
            </li>
          {% endif %}
        {% endfor %}
      </ul>
    </div>
  </div>
</div>

<p class="all-projects-link"><a href="{{ '/publications/' | relative_url }}">Browse all publications &rarr;</a></p>
