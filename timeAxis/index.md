---
layout: home
---

<div class="index-content timeAxis">
    <div class="section">
        <ul class="artical-cate">
            <li><a href="/"><span>Blog</span></a></li>
            <li class="on" style="text-align:center"><a href="/timeAxis"><span>时光轴</span></a></li>
            <li style="text-align:right"><a href="/aboutMe"><span>个人简介</span></a></li>
        </ul>

        <div class="cate-bar"><span id="cateBar"></span></div>

        <div class="artical-list archive">
		
        {% for post in site.categories.blog %}
		<article>
			<h3 class="year">{{ post.date | date: "%Y" }}</h3>
			<section>
				<span class="point-time "></span>
				<time datetime="{{ post.date | date: "%m" }}-{{ post.date | date: "%d" }}">

				<span>{{ post.date | date: "%m" }}月{{ post.date | date: "%d" }}日</span>
				<span></span>
				</time>
				<aside>
					<p class="things"><a href="{{ post.url }}">{{post.title}}</a></p>

				</aside>
			</section>
		</article>
        {% endfor %}
		</div>
		
    </div>
    <div class="aside">
    </div>
</div>
