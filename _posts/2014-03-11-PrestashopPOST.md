---
title: Prestashop Back Office Module GET vs POST
tags: prestashop
layout: post
---

If you've been trying to get Prestashop to wire up you're *AdminController*
you may have ran into the same problem as me. For example, a form like this:

    <form action="index.php?controller=AdminSomething&amp;token={$token}">

Now when the form submits you'll notice it does not go to `AdminSomething` but
instead back to `AdminDashboard`, which is not what we want. However, if you
change this to a `POST` it will work, which is a bit odd:

    <form method="POST" action="index.php?controller=AdminSomething&amp;token={$token}">

Hopefully this helped someone :)
