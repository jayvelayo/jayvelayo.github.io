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
Building robots have always been a passion of mine. There's nothing more satisfying than designing, testing, and deploying completed designs that aims to enhance performance, stability, and efficiency. My involvement in student design teams, and previous work experience has shaped me to become an analytical and dependable engineer. I always give full attention to details in every project lifecycle to ensure that technical functionalities are met.

I'm eager to tackle new challenges that I will undoubtably will face. I'm looking for a role where I'm able to solve real-world problems with logical and innovative solutions. As a fresh graduate, I'm excited to learn from more experienced members and be able to contribute in the industry. I'm also not afraid to work in a hands-on setting, whether it'll be in an instrumentation lab or machine shop setting. 

## Technical Skills
* Programming: C/C++, C#, MATLAB, Assembly, Visual Basic, .NET
* System Design: Digital Control Systems, Concurrent Programming, OS Design, Control Theory
* Hardware Design: Arduino, MSP430, I2C, SPI, UART, Motors, Sensors
* Software: Visual Studio, Code Composer Studio, SolidWorks, KiCAD, Excel VBA
* Project Management: Git, SVN, UML, Jira, JDEdwards

## Interests
* **Self driving cars** - It's a new and upcoming technology which I think will create a lasting impact technologically and socially.
* **Sustainable / Alternate Energy** - With the growing need for power production, I'm interested in the use of sustainable energy sources which benefits the global ecosystem.
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
