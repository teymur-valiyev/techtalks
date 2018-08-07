---
author: teymur
comments: true
date: 2019-04-09 00:00:00+00:00
layout: post
slug: package-manager
title: Package Manager
categories: Tutorial
tags:
- linux
- package-manager
---

/etc/ and /etc/init.d/ directories; by using packages, distributions are able to enforce a single standard.


The Debian package management system, based on a tool called dpkg with the very popular apt system.

debs packaged for Debian are often compatible with Ubuntu

apt-get, a command which uses the advanced packaging tool to interact with the operating system’s package system.

apt-get update - Reads the /etc/apt/sources.list file and updates the system’s database of packages available for installation. Run this after changing sources.list.


/etc/apt/sources.list
The file /etc/apt/sources.list controls repositories from which APT constructs its database. 

dpkg -i package-file-name.deb - Installs a .deb file.
dpkg --list search-pattern - Lists packages currently installed on the system.
dpkg --configure package-name(s) - Runs a configuration interface to set up a package.
dpkg-reconfigure package-name(s) - Runs a configuration interface on an already installed package

/etc/yum.confPermalink
The file located at /etc/yum.conf provides system-wide configuration options for YUM, as well as information about repositories. Repository information may also be located in files ending in .repo under /etc/yum.repos.d.


gpg (GNU Privacy Guard) is the tool used in secure apt to sign files and check their signatures.

apt-key is a program that is used to manage a keyring of gpg keys for secure apt. The keyring is kept in the file /etc/apt/trusted.gpg (not to be confused with the related but not very interesting  /etc/apt/trustdb.gpg). apt-key can be used to show the keys in the keyring, and to add or remove a key.