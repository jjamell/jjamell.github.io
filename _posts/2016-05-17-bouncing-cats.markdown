---
layout: post
title:  "Bouncing Cats"
date:   2016-05-17 01:35:00
categories: github portfolio
---

![Screenshot](/images/bouncingcats.png)

[Bouncing Cats live demo](http://jjamell.github.io/Cat-Thing/)

This is a technical demo of sorts.  Not particularly useful in production but it was fun coding the different components that are wired together that make this work.

A theoretical infinite number (to the extent that your CPU can handle) of objects can be spawned, as each object is independent of one another.  They have update and draw methods that are called by the main loop.  It tries to stay mostly ignorant of what these objects are and what they do.

{% highlight javascript %}
//called on every requestAnimationFrame(), up to 60 frames per second at the browser's discretion.
for (var x in this.gameObjects) {
	if (this.gameObjects[x].draw) {
		this.gameObjects[x].draw(dt, this.backBufferContext2D, this.xScroll, this.yScroll);
	}
}
{% endhighlight %}

That's it.  That's the game loop.  Pretty simple, huh?  Every object has a pretty simple drawing method at the moment, since they're just square images on a 2D canvas.

{% highlight javascript %}
this.draw = function(/**Number*/ dt, /**CanvasRenderingContext2D*/ context, /**Number*/ xScroll, /**Number*/ yScroll)
{
	context.drawImage(this.image, this.x - xScroll, this.y - yScroll);
}
{% endhighlight %}

Making them move is a little bit more complicated.  Currently each object searches for all other colliding objects within the gameObjects stack, though I'd like to optimize this later with space partitioning.  I may go into more detail on how that works in another post.

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
[gh-bouncing-cats]: http://jjamell.github.io/Cat-Thing/