---
title: 'Lightsail, Bitnami and SSH'
date: '2022-01-28T08:25:28-06:00'
author: Brett
layout: single 
categories:
    - Technology
---

This blog runs in Lightsail on WordPress with a Certified by Bitnami instance. Lately, I’ve run into the following when trying to ssh in from the Lightsail console:

<figure class="wp-block-image size-full">![](https://www.anexperimentwithoutscotch.com/wp-content/uploads/2022/01/Screen-Shot-2022-01-28-at-8.21.34-AM.png)</figure>This hangs forever. A couple of times, a reboot of the instance seemed to fix it but this morning, nothing changed the behavior. So I decided to try to ssh from the terminal and lo and behold, this works. You have to download your private keys from your Lightsail account and then following [these instructions](https://lightsail.aws.amazon.com/ls/docs/en_us/articles/amazon-lightsail-ssh-using-terminal) worked fine from the terminal. This will probably be my default going forward.