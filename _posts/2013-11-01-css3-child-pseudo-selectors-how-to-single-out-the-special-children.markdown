---
layout: post
title: "CSS3 Child Pseudo-Selectors: How To Single Out the Special Children"
date: 2013-11-01
comments: true
categories: CSS
published: true

---
When working with HTML lists, there will be a time when you want to modify the styles for the first or last item in the list. For example, maybe you increase the margin between each item, but also need an additional buffer before the first item or after the last item in the list. 

This has traditionally been solved using special CSS classes that are applied to only the first and last items in the list. But wouldn't it be nice if the HTML markup only had to worry about the content and your styles could deal with selecting and styling the first/last items in the list?  

Enter the CSS3 selectors of ["first-child"](https://developer.mozilla.org/en-US/docs/Web/CSS/:first-child) and ["last-child"](https://developer.mozilla.org/en-US/docs/Web/CSS/:last-child).  These selectors aren't anything new as they have been part of the CSS3 spec for years.  But I find this design pattern coming in handy frequently, so it's worth repeating here.  

For the examples below, let's use an unordered list of items. In this case, our items are characters from Game of Thrones. 
{% highlight html %} 
<div class="hero-unit">
  <p>Game of Thrones Selector Fun</p>
  <ul>
    <li>Tyrion</li>
    <li>Jaime</li>
    <li>Cersei</li>
    <li>Daenerys</li>
    <li>Jon</li>
    <li>Tywin</li>
    <li>Bran</li>
  </ul>
</div>
{% endhighlight %}

###first-child, last-child 
The pseudo-selectors of "first-child" and "last-child" give that additional level of control for styling just the first or last elements in a collection of child elements, and let you do that without cluttering up your markup with additional classes.  

For example, using the "last-child" selector, you can easily modify the bottom margin of the last item in the list to match the top margin that is already applied to all of the items in the list.  

{% highlight css %} 
ul {
    border: 1px solid black;
    list-style-type: none;
}

li {
    margin-top: 10px;
}

li:last-child { 
    margin-bottom: 10px;
}
{% endhighlight %}

###nth-child
The ["nth-child"](https://developer.mozilla.org/en-US/docs/Web/CSS/:nth-child) pseudo-selector gives you even more control, allowing you to select a specific occurrence of a child element.  Let's say you want to style the background color of the 2nd item in the list.  No big deal with the "nth-child" pseudo-selector. Just remember that the first item in the list is element 1 - no zero based lists here!

{% highlight css %} 
ul {
    border: 1px solid black;
    list-style-type: none;
}

li {
    margin-top: 10px;
}

li:last-child { 
    margin-bottom: 10px;
}

li:nth-child(2) { 
    background-color: #C0C0C0;
}
{% endhighlight %}


###Even and Odd Children
For our Game of Thrones character list, just changing the background color of the 2nd item in the list isn't that useful. But, we can use the same pseudo-selector to style the background color of all of the even/odd items in the list.  To do this, we use the "even" or "odd" keyword with the nth-child selector to select just the even/odd items.  

{% highlight css %} 
ul {
    border: 1px solid black;
    list-style-type: none;
}

li {
    margin-top: 10px;
}

li:last-child { 
    margin-bottom: 10px;
}

li:nth-child(even) {
    background-color: #C0C0C0; 
}
{% endhighlight %}

###Browser Support
Whenever we discuss CSS, it's worth reviewing the browser support for these [selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference). As of this time, all of these selectors are supported in the latest versions of the major desktop and mobile browsers, but some browsers (a'hem - IE) did not support all of these selectors until more recently. For example, IE has supported the "first-child" selector since IE7, but did not add support for "last-child" or "nth-child" until IE9.
