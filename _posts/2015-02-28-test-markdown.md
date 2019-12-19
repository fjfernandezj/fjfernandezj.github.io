---
layout: post
title: ¿y...cuál su gracia?
subtitle: Each post also has a subtitle
gh-repo: daattali/beautiful-jekyll
gh-badge:
  - star
  - fork
  - follow
tags:
  - test
comments: true
published: true
---

Mi nombre es Francisco Fernández, Economista agrario y de los recursos naturales, profesor de Economía Aplicada Sectorial y Métodos Estadísticos de la Escuela de Agronomía de la Universidad Mayor. Mis principales intereses se relacionan con el desarrollo de herramientas cuantitativas que apoyen a la toma de decisiones del sector agropecuario y  otros sectores económicos relacionados con recursos naturales. Entre ellos, el desarrollo de modelos que permitan analizar los probables impactos económicos del cambio climático en la agricultura nacional o la evaluación ex-ante de políticas de desarrollo y adaptación del sector.

**Here is some bold text**

## Here is a secondary heading

Here's a useless table:

| Number | Next number | Previous number |
| :------ |:--- | :--- |
| Five | Six | Four |
| Ten | Eleven | Nine |
| Seven | Eight | Six |
| Two | Three | One |


How about a yummy crepe?

![Crepe](https://s3-media3.fl.yelpcdn.com/bphoto/cQ1Yoa75m2yUFFbY2xwuqw/348s.jpg)

It can also be centered!

![Crepe](https://s3-media3.fl.yelpcdn.com/bphoto/cQ1Yoa75m2yUFFbY2xwuqw/348s.jpg){: .center-block :}

Here's a code chunk:

~~~
var foo = function(x) {
  return(x + 5);
}
foo(3)
~~~

And here is the same code with syntax highlighting:

```javascript
var foo = function(x) {
  return(x + 5);
}
foo(3)
```

And here is the same code yet again but with line numbers:

{% highlight javascript linenos %}
var foo = function(x) {
  return(x + 5);
}
foo(3)
{% endhighlight %}

## Boxes
You can add notification, warning and error boxes like this:

### Notification

{: .box-note}
**Note:** This is a notification box.

### Warning

{: .box-warning}
**Warning:** This is a warning box.

### Error

{: .box-error}
**Error:** This is an error box.
