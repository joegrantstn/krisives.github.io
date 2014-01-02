---
title: PrestaShop CarrierModule Troubleshooting
tags: php prestashop
layout: post
---

PrestaShop can be extended and configured to do a lot of stuff, which is pretty
awesome but also can be a headache with some documentation missing. When creating
a simple `CarrierModule` I had a lot of issues taht didn't seem related to anything
I was doing - but more quirks of how the module system worked.

## Why doesn't my carrier module display as installable after uploading?

This means the `config.xml` is missing/invalid or that you didn't format
the `.zip` file correctly when uploading it. The PrestaShop 1.5 documentation
explains the structure, but doesn't describe how the contents of the package
file should contain a *sub-directory* of the module contents. If your module
name was `mymodule` then it would contain a directory inside the `.zip` file
called `mymodule`, with a PHP class file at `mymodule/mymodule.php`

## Why doesn't my carrier module install?

The most likely case here is you have implemented `install()` for the
`CarrierModule` but not invoked the `parent::install()` method, which
does the work for saving to the database, etc. You must also `return true`
for the install method to succeed.

When testing your module check the `ps_module` table. Your module is
not really installed until it has a row in that table.

If you have module-specific things happening during the install it's
possible they are failing before calling `parent::install()`

(The most irritating part about this error is that PrestaShop will tell
you the module has been installed successfully, when it has not)

## Why doesn't my carrier display during checkout?

By default PrestaShop will display external carriers that meet this SQL condition:

	(c.is_module = 0 OR c.need_range = 1)

An external carrier that sets `need_range` to zero will never be seen, at least in
my experience. In your install() method when creating the carrier you'll probably
want to do this:

	$carrier->need_range = true;

## Why does the ps_carrier table create duplicates?

For order history it appears that changes to carriers are not made directly
to rows in the table, since that would break previous order history. Instead
each time a carrier is changed a new row is inserted, with `id_reference` describing
the actual carrier.


## What have you had problems with?

Let me know what problems you are having maybe I can help and add the problem
to this article.
