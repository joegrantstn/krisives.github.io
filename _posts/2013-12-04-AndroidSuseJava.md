---
title: OpenSuse 12.3, Android SDK, and Oracle Java
tags: linux android
layout: post
---

Are you getting strange crashes when you try to use the Android SDK
on OpenSuse 12.3? For me I would get a crash whenever I ran the emulator,
and it was actually crashing before running the AVD image. Inspecting
the stack trace shows it was related to AWT/SWT widgets not being
available like they should have been. That's a big red flag in my
book and reminds me to check...

What version of Java am I running? It's not terribly important for
basic command line applications, but once the GUI is involved and
especially JNI based libraries, the open source implementation of
Java is either inferior or just incompatibile. To see what version
you are running:

    java -version

If you're on the default GCJ version it will also let you use the
`--version` flag, although the default Oracle JDK only accepts the
single dash `-version` flag.

Once you realize you're running GCJ grab Oracle's JRE instead. It's
really easy to install yourself by extracting, but we have a 1-click
that works great:

[One Click Installer for Oracle JRE
](http://software.opensuse.org/download.html?project=home%3Anesnomis&package=oracle-jre7-java-installer)


Yay now Java works and you can get back to *real work*
