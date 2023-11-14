---
layout: aboutme
title: About Me
description: A description about my journey, interests, and other fun quirks. 
---

## Biography

I am a cool guy. I'll write more later on :D

<body>
<div id="slideshow">
	<img src="http://placehold.it/300x200&text=foo1.jpg">
	<img src="http://placehold.it/300x200&text=foo2.jpg" style="display: none">
	<img src="http://placehold.it/300x200&text=foo3.jpg" style="display: none">
	<img src="http://placehold.it/300x200&text=foo4.jpg" style="display: none">
	<img src="http://placehold.it/300x200&text=foo5.jpg" style="display: none">
</div>
<script>
var slideshow = document.getElementById('slideshow');
var slides = slideshow.getElementsByTagName('img');
var idx = 0;
function changeSlide() {
	slides[idx].style.display = 'none';
	idx = (idx + 1) % slides.length;
	slides[idx].style.display = 'block';
}
setInterval(changeSlide, 3000);
</script>
</body>