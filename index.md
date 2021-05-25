---
layout: default
---

<div id="main">
  <article>
    <header>
      <h1 class="post-title">{{ page.title }}</h1>
      <p class="post-meta">{{ page.date | date: "%b %-d, %Y" }}{% if page.author %} • {{ page.author }}{% endif %}{% if page.meta %} • {{ page.meta }}{% endif %}</p>
    </header>

<section>
<div class="info" markdown="1">  

## Introduction

As a Software engineer, my passion lies in working with embedded systems. In my 3+ years experience writing real-time, multithreaded software, I apply the most suitable software design patterns to create products that promotes excellence and efficiency. I have hands-on experience working with microcontrollers namely ARM Cortex M7, and programming network sockets such as TCP/IP. My peers and managers have complimented my work ethics, particularly my independence and communication skills. I strive to surpass expectations by using my attention to detail to optimize even the smallest components. I'm always looking for new opportunities to translate my experience and knowledge to solve real-world problems with logical and innovative solutions.


## Technical Skills
* Programming: C, C++, Python, Assembly, C#, Visual Basic
* System Design: Real-time Design, Concurrent Programming, Control Theory, Digital Systems Design
* Hardware Design: ARM Cortex M7, Arduino, MSP430, ESP8266 WiFi Module, Socket Programming, Serial Communications, Motors, Sensors
* Software: Visual Studio, Code Composer Studio, Excel VBA
* Project Management: Git, SVN, UML, Jira, Redmine

## Interests
* **Sustainable / Alternate Energy** - With the growing need for power production, I'm interested in the use of sustainable energy sources to reduce the carbon emission in the world
* **Physical Fitness** - Working on my physical health has improved my discipline and work ethics to meet my personal goals
* **Outdoor Activities** - Living in Vancouver where it boasts the most beautiful scenery, I take my chance to explore nature and take part in outdoor activities.

## Projects

</div>	  
    </section>
    <section>
      <footer>
        <div class="row">
        {% for post in site.posts %}
        <article class="{% cycle '6u', '6u$' %} 12u(small) excerpt">
          <header>
            <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
          </header>
          <section>
            {{ post.excerpt }}
          </section>
          <footer>
            <ul class="actions">
              <li><a href="{{ post.url }}" class="button">Read More</a></li>
            </ul>
          </footer>
        </article>
        {% endfor %}  
        </div>
      </footer>
    </section>
  </article>
</div>
