---
layout: page
permalink: /students/
title: Students
description: 
nav: true
nav_order: 2
---
I supervise students' research in a structured manner, with clear goals for both **short-term exploration** and **long-term deep dive**. My aim is to keep everyone engaged with the latest advancements in the field, while helping my graduate students stay focused on their core research problems. To support this, _I involve many undergraduate students in exploratory projects_ focused on emerging algorithms. This creates a collaborative environment where knowledge is shared across the lab and students learn from one another.

## Graduate Students
<div class="student-section">
  {% for student in site.data.grad_students %}
  <div class="student-row">
    <div class="student-image">
      <img src="../assets/images/students/{{ student.image }}" alt="{{ student.name }}">
    </div>
    <div class="student-info">
      {% if student.linkedin %}
      <a href="{{ student.linkedin }}" target="_blank" class="student-name-link">
        <strong class="student-full-name">{{ student.name }}</strong>
      </a>
      {% else %}
      <strong class="student-full-name">{{ student.name }}</strong>
      {% endif %}
      <div class="student-details">{{ student.program }}</div>
      {% if student.cosupervisor %}
      <div class="student-details">Co-sup. with {{ student.cosupervisor }}</div>
      {% endif %}
    </div>
  </div>
  {% endfor %}
</div>

## Research Assistants
<div class="student-section">
  {% for student in site.data.research_assistants %}
  <div class="student-row">
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
  {% assign all_terms = "Spring 2025,Winter 2025,Fall 2024,Spring 2024,Winter 2024,Fall 2023,Spring 2023,Winter 2023,Fall 2022" | split: "," %}
  {% for term in all_terms %}
    {% assign students_in_term = site.data.undergrads | where_exp: "student", "student.terms contains term" %}
    {% if students_in_term.size > 0 %}
      <div class="term-container">
        <h3 class="term-header" onclick="toggleTerm(this)">
          <span class="term-title">{{ term }}</span>
          <span class="toggle-icon">▼</span>
        </h3>
        <div class="term-group">
          {% for student in students_in_term %}
            {% assign latest_term = student.terms | split: "," | first | strip %}
            {% if latest_term == term %}
              <div class="student-row undergrad-row">
                {% if student.image %}
                <div class="student-image undergrad-image">
                  <img src="../assets/images/students/{{ student.image }}" alt="{{ student.name }}">
                </div>
                {% endif %}
                <div class="student-info">
                  {% if student.linkedin %}
                  <a href="{{ student.linkedin }}" target="_blank" class="student-name-link">
                    <strong class="student-full-name">{{ student.name }}</strong> {{ student.type }}{% if student.major %} ({{ student.major }}){% endif %}
                    {% assign terms_array = student.terms | split: "," %}
                    {% if terms_array.size > 1 %}
                    <div class="student-terms">Terms: {{ student.terms }}</div>
                    {% endif %}
                  </a>
                  {% else %}
                  <strong class="student-full-name">{{ student.name }}</strong> {{ student.type }}{% if student.major %} ({{ student.major }}){% endif %}
                  {% assign terms_array = student.terms | split: "," %}
                  {% if terms_array.size > 1 %}
                  <div class="student-terms">Terms: {{ student.terms }}</div>
                  {% endif %}
                  {% endif %}
                  <div class="student-details research-field undergrad-details">{{ student.research }}</div>
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

<style>
.student-section {
    margin-bottom: 2em;
}

.term-header {
    margin-top: 1.5em;
    margin-bottom: 0.5em;
    color: #333;
    font-size: 1.2em;
    border-bottom: 2px solid #eee;
    padding-bottom: 0.3em;
}

.term-group {
    margin-left: 1em;
    border-left: 2px solid #f0f0f0;
    padding-left: 1em;
}

.student-row {
    display: flex;
    align-items: flex-start;
    margin-bottom: 1.5em;
    padding-bottom: 1em;
    border-bottom: 1px solid #eee;
}

/* Specific styles for undergraduate section */
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

.undergrad-image {
    width: 80px;
    height: 80px;
    margin-right: 1em;
}

.student-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 50%;
}

.student-info {
    flex-grow: 1;
}

.student-name-link {
    text-decoration: none;
    color: inherit;
}

.student-name-link:hover {
    text-decoration: underline;
}

.student-details {
    color: #666;
    margin: 0.3em 0;
    font-size: 0.95em;
}

.undergrad-details {
    margin: 0.2em 0;
    font-size: 0.9em;
}

.research-field {
    font-style: italic;
}

.paper-link {
    color: #0366d6;
    text-decoration: none;
}

.paper-link:hover {
    text-decoration: underline;
}

.paper-link i {
    margin-right: 0.3em;
}

/* Updated styles for collapsible terms */
.term-container {
    margin-bottom: 1em;
}

.term-header {
    cursor: pointer;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0.5em 1em;
    background-color: #f8f9fa;
    border-radius: 4px;
    transition: background-color 0.2s;
    margin-bottom: 0.5em;
}

.term-header:hover {
    background-color: #e9ecef;
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
    border-left: 2px solid #f0f0f0;
    padding-left: 1em;
    transition: all 0.3s ease-out;
    max-height: 2000px; /* Large enough to contain content */
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

.student-terms {
    color: #666;
    font-size: 0.9em;
    margin-top: 0.2em;
}
</style>

<script>
function toggleTerm(header) {
    const termGroup = header.nextElementSibling;
    const isCollapsed = header.classList.contains('collapsed');
    
    if (isCollapsed) {
        header.classList.remove('collapsed');
        termGroup.classList.remove('collapsed');
        // Set the actual height after removing collapsed class
        termGroup.style.maxHeight = termGroup.scrollHeight + 'px';
    } else {
        header.classList.add('collapsed');
        termGroup.classList.add('collapsed');
        termGroup.style.maxHeight = '0';
    }
}

// Initialize all terms as expanded
document.addEventListener('DOMContentLoaded', function() {
    const termHeaders = document.querySelectorAll('.term-header');
    termHeaders.forEach(header => {
        const termGroup = header.nextElementSibling;
        termGroup.style.maxHeight = termGroup.scrollHeight + 'px';
    });
});
</script>

<!-- Font Awesome for paper icon -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">

## Lab Photos
<div class="lab-photos">
  <div class="photo-container">
    <img src="../assets/images/lab_photo.png" alt="Lab Group Photo" class="lab-photo">
    <div class="photo-caption">Our lab group in Spring 2024</div>
  </div>
</div>

<style>
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
    box-shadow: 0 4px 8px rgba(0,0,0,0.1);
}

.photo-caption {
    margin-top: 1em;
    color: #666;
    font-style: italic;
}
</style> 