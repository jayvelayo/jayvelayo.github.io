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
Building robots have always been a passion of mine. There's nothing more satisfying than designing, testing, and deploying completed designs that aims (to ease up workflow). I strive to combine what I know from UBC Mechatronics and to what I can achieve.

I'm eager to tackle new challenges that I will undoubtably will face. I'm looking for a role where I'm able to solve real-world problems with (clean) and creative solutions. As a fresh graduate, I'm excited to work with other experienced members where I am able to share/contribute and (absorb) (knowledge). I'm also not afraid to take on a leadership role, where I can show my (responsibilitiness) (responsibilities = leadership?). 

## Highlights
* 

## Interests
* **Self driving cars.** It's a new and upcoming technology which I think will create a lasting impact in terms of technologically and socially.
* **Video Games.** Should I even say this? LOL
* **Outdoor Activities.** Living in beautiful Vancouver, I take my chance to explore the nature and parks around the area.

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
