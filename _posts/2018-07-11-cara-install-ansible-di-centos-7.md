---
layout: post
title: "Cara Install Ansible di Centos 7"
date: 2018-07-11 15:07:19
categories: [Linux]
tags: [Ansible]
comments: true
---

Pada kesempatan kali ini saya akan membahas bagaimana cara install `Ansible` di `Centos 7`. Kemudian apa sih `Ansible` itu ?? `Ansible` adalah  sebuah software atomasi yang digunakan untuk mengelola server dalam jumlah yang cukup banyak. `Ansible` pada umumnya bekerja seperti tools lain , semacam Chef, Puppet, hanya saja `Ansible` tidak membutuhkan agent. Ansible hanya bekerja cukup dengan koneksi SSH.

<!--more-->


## Sistem Operasi dan versi Ansible
   * **Sistem Operasi**: CentOS Linux release 7.5.1804 (Core)
   * **Software**: ansible 2.5.5


## Persyaratan
Akses root ke Sistem Operasi Centos

## Instalasi
Untuk menginstall `Ansible` di `Centos 7` kita bisa menggunakan Repositori **EPEL**.

{% highlight python %}
   $ sudo yum -y install epel-release
   $ sudo yum -y update
{% endhighlight %}

Selanjutnya, install `Ansible`

{% highlight python %}
   $ sudo yum -y install ansible
{% endhighlight %}

Jika sudah di install dengan benar, seharus nya kita bisa menggunakan perintah `ansible` untuk query versinya:

{% highlight python %}
   $ sudo ansible --version
   ansible 2.5.5
   config file = /etc/ansible/ansible.cfg
   ..
{% endhighlight %}

Demikianlah cara install `Ansible` di `Centos 7`. Untuk tutorial berikut nya kita akan bahas bagaimana konfigurasi **Host** dan **Ansible Playbok**


## Referensi
   * [https://www.ansible.com/](https://www.ansible.com/)
