---
layout: post
title: "Tutorial Konfigurasi Pure-Ftpd di Linux"
date: 2018-01-08 15:07:19
categories: [Linux]
tags: [ftp, Pure-fptd]
comments: true
---

Pada artikel kali ini kita akan bahas tentang tutorial konfigurasi pure-ftpd di linux. Pureftpd sendiri bersifat free dan berfokus pada efisiensi dan kemudahan dalam penggunaannya. Ini memberikan jawaban sederhana untuk kebutuhan umum, ditambah fitur unik yang berguna untuk pengguna pribadi maupun penyedia hosting.

<!--more-->

## Instalasi
Step 1: kita mulai dengan menginstall pake pure-ftpd
{% highlight python %}
pada Centos, RedHat:
   # yum -y install pure-ftpd

pada Ubuntu, Debian:
   # apt -y install pure-ftpd
{% endhighlight %}

## Konfigurasi
Step 2: Edit berkas konfigurasi pure-ftpd

{% highlight ruby %}
   # vi /etc/pure-ftpd/pure-ftpd.conf
{% endhighlight %}

{% highlight ruby %}
   ChrootEveryone              yes
   MaxClientsNumber            50
   MaxClientsPerIP             2
   VerboseLog                  yes
   AnonymousOnly               no
   NoAnonymous                 yes
   PAMAuthentication no
   PureDB /etc/pure-ftpd/pureftpd.pdb
{% endhighlight %}

Step 3: service pure-ftpd
{% highlight ruby %}
   # systemctl enable pure-ftpd
   # systemctl start pure-ftpd
{% endhighlight %}

## Menambahkan User
Step 4: membuat user baru dengan perkakas pure-pw
{% highlight ruby %}
   # pure-pw useradd $USERNAME -u $USER -g $GROUP -d /path/to/ftp/directory
   # pure-pw
{% endhighlight %}

> $USERNAME : Username ftp.
>
> $USER : System Username ( seperti nginx, apache, www-data dll).
>
> $GROUP : System Group name ( seperti nginx, apache, www-data dll).

Untuk mengganti password user pure-ftpd

{% highlight ruby %}
   # pure-pw passwd $USERNAME
   # pure-pw mkdb
{% endhighlight %}

## Done
Demikian Tutorial Konfigurasi Pure Ftpd Di Linux, semoga dapat berguna.
