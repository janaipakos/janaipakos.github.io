---
layout: post
title:  Avoid Redundancy in Django
date: 2016-01-22
---

Django's template inheritance shines when using different designs for different users. This is thanks to Django's `block.super` template object, which reduces overhead and avoids the the need to create multiple base files.

Say you are building a project with one design for most users, and a dashboard with a different design for administrative users. Most developers would create a base.html file and a base.dashboard.html file. However, we now have two architectures to maintain, and this can bloat quickly as more users and designers are added.

Luckily, Django has the `block.super` object, which ensures the parent content is included in the block when it is placed in the child template's block. This means you can still override the base content with `% block %` while also ensuring the content you want is included with `block.super`.

An easy way to picture this object is a Hawthorne cocktail strainer, which has a adjustable seive. The bartender, or user, can adjust how much ice, or base content, leaks into the finished prodict.

Here's what it looks like:

    {% raw %}
    {% extends "base.html" %}
    {% block stylesheets %}
      {{ block.super }}
      <link rel="stylesheet" type="text/css" href="{% static "css/custom" %}" />
    {% endblock %}
    {% endraw %}

The above code will bring in the css from the base file and include a custom stylesheet. No overriding or duplication.

This is a pretty easy fix to project redundancy. It came from the awesome book [*Two Scoops of Django*](https://www.twoscoopspress.com/products/two-scoops-of-django-1-8) (Daniel Roy Greenfeld, Audrey Roy Greenfeld, 2015).
