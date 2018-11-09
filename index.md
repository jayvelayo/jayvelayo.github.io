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
Building robots has always been a passion of mine. There's nothing more satisfying than designing, testing, and deploying completed designs that aim to enhance performance, stability, and efficiency. My involvement in student design teams, and previous work experience have shaped me to become an analytical and dependable engineer. I always give my full attention to details in every project lifecycle to ensure that technical functionalities are met.

My passion lies in programming embedded systems using C or C++. I aspire to use my skills in concurrency and real-time system design to create products that can meet functional requirements in an effective manner. In my free time, I use these skills to create simple yet meaningful designs that showcases my understanding. Therefore, I'm looking for an opportunity to translate my experience into products that aim to solve real-world problems with logical and innovative solutions. As a fresh graduate, I'm excited to learn from more experienced members and be able to contribute to the industry. I'm also not afraid to work in a hands-on setting, whether it be in an instrumentation lab or in a machine shop setting. 

## Technical Skills
* Programming: C/C++, Assembly, C#, Python, MATLAB, Visual Basic
* System Design: Real-time Design, Concurrent Programming, Control Theory, Digital Systems Design
* Hardware Design: Arduino, MSP430, ESP8266 WiFi Module, I2C, SPI, UART, Motors, Sensors
* Software: Visual Studio, Code Composer Studio, KiCAD, SolidWorks, Excel VBA
* Project Management: Git, SVN, UML, Jira

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
