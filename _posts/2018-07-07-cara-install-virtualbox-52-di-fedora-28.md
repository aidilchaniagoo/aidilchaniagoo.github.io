---
category: Linux
---

`Oracle VM VirtualBox` adalah perangkat lunak virtualisasi, yang dapat digunakan untuk mengeksekusi sistem operasi "tambahan" di dalam sistem operasi "utama".


Virtualbox mendukung hampir sejumlah besar dari guest operating systems:


   * Windows 3.x
   * Windows NT 4.0
   * Windows 2000
   * Windows XP
   * Windows Server 2003
   * Windows Server 2008
   * Windows Vista
   * Windows 7
   * Windows 8
   * Windows 8.1
   * Windows 10
   * DOS
   * Linux (Kernel 2.4, 2.6, 3.0, 3.2, 3.4, 3.10, 3.16, 3.18, 4.1, 
     4.4, 4.7, 4.8, 4.9, 4.10, 4.11, 4.12, 4.13, 4.14, 4.15, 4.16)
   * Solaris
   * OpenSolaris
   * OpenBSD



Pada artikel kali ini kita akan membahas bagaimana Cara Install Virtualbox 52 Di Fedora 28

## Repository
Step 1: Tambahkan repository virtualbox
{% highlight python %}
   $ sudo wget http://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repo -P /etc/yum.repos.d/
{% endhighlight %}


## Update 
Step 2: Setelah menambahkan repository virtualbox lakukan update
{% highlight python %}
   $ sudo dnf -y update
{% endhighlight %}

Kemudian pastikan OS berjalan di kernel yang terbaru.

{% highlight python %}
   $ sudo rpm -qa kernel |tail -n 1 |sed 's/kernel-//g'
   output: 4.17.3-200.fc28.x86_64

   $ sudo uname -ra
   output: 4.17.3-200.fc28.x86_64
{% endhighlight %}

`note:` jika mendapatkan update kernel, atau OS sedang berjalan pada kernel lama maka lakukan restart.

{% highlight python %}
   $ sudo shutdown -r now
{% endhighlight %}


## Paket Dependensi
Step 3: Berikut ini adalah paket yang di butuhkan untuk menginstall VirtualBox 5.2 di Fedora 28
{% highlight python %}
   $ sudo dnf install binutils gcc make patch libgomp \
     glibc-headers glibc-devel kernel-headers kernel-devel dkms
{% endhighlight %}


## VirtualBox 5.2
Step 3: Install paket VirtualBox 
{% highlight python %}
   $ sudo dnf install VirtualBox-5.2
{% endhighlight %}


Rebuild kernel modules dengan perintah di bawah ini
{% highlight python %}
   $ /usr/lib/virtualbox/vboxdrv.sh setup
{% endhighlight %}

Perintah di atas secara otomatis akan membuat group `vboxusers` dan user yang akan menjalankan virtualbox haruslah member dari group tersebut. maka jalankan perintah berikut untuk menambahkan user menjadi members dari group `vboxusers`.

{% highlight python %}
   $ usermod -aG vboxusers User_Kalian
{% endhighlight %}

