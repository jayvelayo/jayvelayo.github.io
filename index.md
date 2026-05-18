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

## Software Engineer – Backend, Distributed Systems, Infrastructure & Networking

I am a Staff Software Engineer specializing in backend and distributed systems, currently building large-scale infrastructure and networking services at Zscaler.

My work focuses on designing and scaling reliable backend systems that process telemetry from millions of devices, power security and networking services, and maintain high availability in distributed environments.

I have experience building distributed data systems, large-scale messaging and caching infrastructure, and performance-critical services across cloud and embedded environments.

My primary programming languages are Go, C/C++, and Python, and I am particularly interested in backend infrastructure, networking systems, and large-scale distributed platforms.

## Technical Skills
* **Languages:** Go, C, C++, Python
* **Distributed Systems:** Paxos, Pub/Sub, High Availability, Caching, Cloud
* **Technologies:** Linux, Docker, Azure, REST APIs, TCP/IP, TLS, PostgreSQL, Redis
* **Tools:** Git, CI/CD, Jira, Confluence

## Interests
* **Board Games & Gaming** - I enjoy both strategy board games and video games as ways to unwind and exercise strategic thinking
* **Fitness** - Staying active keeps me disciplined and focused, both in and out of work
* **Badminton** - A sport I play regularly to stay competitive and sharp

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
