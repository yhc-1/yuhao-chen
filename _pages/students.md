---
layout: page
permalink: /students/
title: Students
description:
nav: true
nav_order: 2
---

I supervise students' research in a structured manner, with clear goals for both **short-term exploration** and **long-term deep dive**. My aim is to keep everyone engaged with the latest advancements in the field, while helping my graduate students stay focused on their core research problems. To support this, _I involve many undergraduate students in exploratory projects_ focused on emerging algorithms. This creates a collaborative environment where knowledge is shared across the lab and students learn from one another.

{% assign phd = site.data.grad_students | where: "program", "PhD" %}
{% assign masc = site.data.grad_students | where: "program", "MASc" %}
{% assign phd_active = phd | where_exp: "s", "s.status != 'inactive'" %}
{% assign masc_active = masc | where_exp: "s", "s.status != 'inactive'" %}

I currently co-supervise **{{ phd_active.size }} PhD** and **{{ masc_active.size }} MASc** students, and have worked with **130 undergraduate** students since 2022.

## Graduate Students

### PhD
<div class="student-section">
  {% for student in phd %}
  <div class="student-row">
    {% include students_avatar.liquid student=student %}
    <div class="student-info">
      {% if student.linkedin %}
      <a href="{{ student.linkedin }}" target="_blank" class="student-name-link">
        <strong class="student-full-name">{{ student.name }}</strong>
      </a>
      {% else %}
      <strong class="student-full-name">{{ student.name }}</strong>
      {% endif %}
      {% if student.status == 'inactive' %}<span class="student-status">(inactive)</span>{% endif %}
      <div class="student-details">{{ student.program }}{% if student.since %} &middot; since {{ student.since }}{% endif %}</div>
      {% if student.cosupervisor %}
      <div class="student-details">Co-sup. with {{ student.cosupervisor }}</div>
      {% endif %}
    </div>
  </div>
  {% endfor %}
</div>

### MASc
<div class="student-section">
  {% for student in masc %}
  <div class="student-row">
    {% include students_avatar.liquid student=student %}
    <div class="student-info">
      {% if student.linkedin %}
      <a href="{{ student.linkedin }}" target="_blank" class="student-name-link">
        <strong class="student-full-name">{{ student.name }}</strong>
      </a>
      {% else %}
      <strong class="student-full-name">{{ student.name }}</strong>
      {% endif %}
      {% if student.status == 'inactive' %}<span class="student-status">(inactive)</span>{% endif %}
      <div class="student-details">{{ student.program }}{% if student.since %} &middot; since {{ student.since }}{% endif %}</div>
      {% if student.cosupervisor %}
      <div class="student-details">Co-sup. with {{ student.cosupervisor }}</div>
      {% endif %}
    </div>
  </div>
  {% endfor %}
</div>

## Graduate Alumni
<div class="student-section">
  {% for student in site.data.grad_alumni %}
  <div class="student-row">
    {% include students_avatar.liquid student=student %}
    <div class="student-info">
      {% if student.linkedin %}
      <a href="{{ student.linkedin }}" target="_blank" class="student-name-link">
        <strong class="student-full-name">{{ student.name }}</strong>
      </a>
      {% else %}
      <strong class="student-full-name">{{ student.name }}</strong>
      {% endif %}
      <div class="student-details">{{ student.program }}{% if student.years %}, {{ student.years }}{% endif %}</div>
      {% if student.cosupervisor %}
      <div class="student-details">Co-sup. with {{ student.cosupervisor }}</div>
      {% endif %}
      {% if student.note %}
      <div class="student-details">{{ student.note }}</div>
      {% endif %}
    </div>
  </div>
  {% endfor %}
</div>

## Research Assistants
<div class="student-section">
  {% for student in site.data.research_assistants %}
  <div class="student-row">
    {% include students_avatar.liquid student=student %}
    <div class="student-info">
      {% if student.linkedin %}
      <a href="{{ student.linkedin }}" target="_blank" class="student-name-link">
        <strong class="student-full-name">{{ student.name }}</strong>
      </a>
      {% else %}
      <strong class="student-full-name">{{ student.name }}</strong>
      {% endif %}
      <div class="student-details">Research Assistant</div>
    </div>
  </div>
  {% endfor %}
</div>

## Undergraduate Students
<div class="student-section undergrad-section">
  {% assign all_terms = "Fall 2026,Spring 2026,Winter 2026,Fall 2025,Spring 2025,Winter 2025,Fall 2024,Spring 2024,Winter 2024,Fall 2023,Spring 2023,Winter 2023,Fall 2022" | split: "," %}
  {% for term in all_terms %}
    {% assign students_in_term = site.data.undergrads | where_exp: "student", "student.terms contains term" %}
    {% if students_in_term.size > 0 %}
      <div class="term-container">
        <h3 class="term-header" onclick="toggleTerm(this)">
          <span class="term-title">{{ term }}</span>
          <span class="toggle-icon">&#9660;</span>
        </h3>
        <div class="term-group">
          {% for student in students_in_term %}
            {% assign latest_term = student.terms | split: "," | first | strip %}
            {% if latest_term == term %}
              <div class="student-row undergrad-row">
                <div class="student-info">
                  {% if student.linkedin %}
                  <a href="{{ student.linkedin }}" target="_blank" class="student-name-link">
                    <strong class="student-full-name">{{ student.name }}</strong> {{ student.type }}{% if student.major %} ({{ student.major }}){% endif %}
                  </a>
                  {% else %}
                  <strong class="student-full-name">{{ student.name }}</strong> {{ student.type }}{% if student.major %} ({{ student.major }}){% endif %}
                  {% endif %}
                  {% assign terms_array = student.terms | split: "," %}
                  {% if terms_array.size > 1 %}
                  <div class="student-terms">Terms: {{ student.terms }}</div>
                  {% endif %}
                  {% if student.research %}
                  <div class="student-details research-field undergrad-details">{{ student.research }}</div>
                  {% endif %}
                  {% if student.paper %}
                  <div class="student-details undergrad-details">
                    <a href="{{ student.paper }}" target="_blank" class="paper-link">
                      <i class="fas fa-file-alt"></i> Publication
                    </a>
                  </div>
                  {% endif %}
                </div>
              </div>
            {% endif %}
          {% endfor %}
        </div>
      </div>
    {% endif %}
  {% endfor %}
</div>

## Lab Photos
<div class="lab-photos">
  <div class="photo-container">
    <img src="{{ '/assets/images/lab_photo.png' | relative_url }}" alt="Lab group photo" class="lab-photo" />
    <div class="photo-caption">Our lab group in Spring 2024</div>
  </div>
</div>

<style>
  .student-section {
    margin-bottom: 2em;
  }

  .student-row {
    display: flex;
    align-items: flex-start;
    margin-bottom: 1.5em;
    padding-bottom: 1em;
    border-bottom: 1px solid var(--global-divider-color);
  }

  .undergrad-row {
    margin-bottom: 0.8em;
    padding-bottom: 0.8em;
  }

  .student-image {
    width: 100px;
    height: 100px;
    margin-right: 1.5em;
    flex-shrink: 0;
  }

  .student-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 50%;
  }

  /* Initials avatar, shown when a student has no photo on file. */
  .student-initials {
    width: 100px;
    height: 100px;
    margin-right: 1.5em;
    flex-shrink: 0;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2em;
    font-weight: 600;
    letter-spacing: 0.03em;
    color: var(--global-theme-color);
    background-color: var(--global-card-bg-color);
    border: 1px solid var(--global-divider-color);
    user-select: none;
  }

  .student-info {
    flex-grow: 1;
    min-width: 0;
  }

  .student-name-link {
    text-decoration: none;
    color: inherit;
  }

  .student-name-link:hover {
    text-decoration: underline;
  }

  .student-details {
    color: var(--global-text-color-light);
    margin: 0.3em 0;
    font-size: 0.95em;
  }

  .student-status {
    color: var(--global-text-color-light);
    font-size: 0.85em;
    font-style: italic;
    margin-left: 0.3em;
    white-space: nowrap;
  }

  .student-terms {
    color: var(--global-text-color-light);
    font-size: 0.9em;
    margin-top: 0.2em;
  }

  .undergrad-details {
    margin: 0.2em 0;
    font-size: 0.9em;
  }

  .research-field {
    font-style: italic;
  }

  .paper-link {
    color: var(--global-theme-color);
    text-decoration: none;
  }

  .paper-link:hover {
    text-decoration: underline;
  }

  .paper-link i {
    margin-right: 0.3em;
  }

  .term-container {
    margin-bottom: 1em;
  }

  .term-header {
    cursor: pointer;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0.5em 1em;
    margin-top: 1.5em;
    margin-bottom: 0.5em;
    font-size: 1.2em;
    color: var(--global-text-color);
    background-color: var(--global-card-bg-color);
    border-radius: 4px;
    transition: background-color 0.2s;
  }

  .term-header:hover {
    background-color: var(--global-hover-color);
  }

  .toggle-icon {
    font-size: 0.8em;
    transition: transform 0.3s;
  }

  .term-header.collapsed .toggle-icon {
    transform: rotate(-90deg);
  }

  .term-group {
    margin-left: 1em;
    border-left: 2px solid var(--global-divider-color);
    padding-left: 1em;
    transition: all 0.3s ease-out;
    max-height: 4000px;
    opacity: 1;
    visibility: visible;
  }

  .term-group.collapsed {
    max-height: 0;
    margin: 0;
    padding: 0;
    border: none;
    opacity: 0;
    visibility: hidden;
  }

  .lab-photos {
    margin-top: 3em;
    text-align: center;
  }

  .photo-container {
    max-width: 800px;
    margin: 0 auto;
    padding: 1em;
  }

  .lab-photo {
    width: 100%;
    height: auto;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }

  .photo-caption {
    margin-top: 1em;
    color: var(--global-text-color-light);
    font-style: italic;
  }

  @media (max-width: 576px) {
    .student-image,
    .student-initials {
      width: 72px;
      height: 72px;
      margin-right: 1em;
    }

    .student-initials {
      font-size: 1.5em;
    }
  }
</style>

<script>
  function toggleTerm(header) {
    const termGroup = header.nextElementSibling;
    const isCollapsed = header.classList.contains("collapsed");

    if (isCollapsed) {
      header.classList.remove("collapsed");
      termGroup.classList.remove("collapsed");
      termGroup.style.maxHeight = termGroup.scrollHeight + "px";
    } else {
      header.classList.add("collapsed");
      termGroup.classList.add("collapsed");
      termGroup.style.maxHeight = "0";
    }
  }

  document.addEventListener("DOMContentLoaded", function () {
    document.querySelectorAll(".term-header").forEach((header) => {
      const termGroup = header.nextElementSibling;
      termGroup.style.maxHeight = termGroup.scrollHeight + "px";
    });
  });
</script>
