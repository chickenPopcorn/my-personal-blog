---
title: "No More Login to Your Mv"
date: 2018-01-26T21:24:26-05:00
tags: ["linux command"]
draft: false
---

# SSH Your VM

While working as software engineer, something I have grown tired of is to log into my virtual machine few times a day. It's not a cumbersome process to add SSH key, but some of my coworkers ignored as well. Below are two commands that will speed up your life every day by a tiny bit.

```sh
cat ~/.ssh/id_rsa.pub | ssh <user>@<hostname> 'umask 0077; mkdir -p .ssh; cat >> .ssh/authorized_keys && echo "Key copied"'
```

or simply use **ssh-copy-id** in the openssh-client package and installed by default

```sh
ssh-copy-id <user>@<hostname>
```

