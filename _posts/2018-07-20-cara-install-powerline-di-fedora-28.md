---
layout: post
title: "Cara install powerline di fedora 28"
date: 2018-07-20 15:07:19
categories: [Linux]
tags: [Powerline, Vim, Tmux]
comments: true
---

Berikut ini adalah tutorial bagaimana cara menginstall powerline di `Fedora 28`. Saya asumsikan kalian sudah paham apa itu `Powerline` dan apa kegunaannya. Namun jika memang belum mengerti dan baru mendengar tentang `Powerline` kalian bisa baca di [sini](https://github.com/powerline/powerline).

<!--more-->


## Software
 * **Sistem Operasi**: Fedora release 28
 * **Powerline**: 2.6-7

## Persyaratan
Akses root ke Sistem Operasi

## Instalasi
Jalankan perintah berikut untuk menginstall `Powerline` pada `Fedora 28`.
{% highlight bash %}                                                                                                                                
   $ sudo dnf install powerline powerline-fonts tmux-powerline vim-powerline
{% endhighlight %}

Jalankan perintah berikut untuk memastikan powerline telah terinstall.
{% highlight bash %}                                                                                                                                
   $ rpm -qa |grep -i powerline
   vim-powerline-2.6-7.fc28.noarch
   powerline-2.6-7.fc28.x86_64
   powerline-fonts-2.6-7.fc28.noarch
   tmux-powerline-2.6-7.fc28.noarch
{% endhighlight %}

## Konfigurasi
### Powerline
Selanjutnya, konfigurasi `Shell Bash` agar menggunakan `Powerline` secara default. Tambahkan Konfigurasi berikut pada berkas `~/.bashrc`
{% highlight bash %}                                                                                                                                
  if [ -f `which powerline-daemon` ]; then
  powerline-daemon -q
  POWERLINE_BASH_CONTINUATION=1
  POWERLINE_BASH_SELECT=1
  . /usr/share/powerline/bash/powerline.sh
  fi
{% endhighlight %}

### Tmux
Untuk seseorang pencadu command line, kalian mungkin sudah mengenal `Tmux`, dengan `Tmux` kalian dapat membagi jendela dan panel pada terminal. dan banyak lagi kemampuan `Tmux` lainnya.

Tambahkan konfigurasi berikut ini pada berkas konfigurasi `~/.tmux.conf`:
{% highlight bash %}                                                                                                                                
   source "/usr/share/tmux/powerline.conf"
{% endhighlight %}


### Vim
jika kalian pengguna `Vim`, maka kalian beruntung. Karena ada plugin yang sangat powerfull yang tersedia untuk `Vim Powerline`
Tambahkan konfigurasi berikut ini pada berkas konfigurasi `~/.vimrc`:
{% highlight bash %}                                                                                                                                
   python3 from powerline.vim import setup as powerline_setup
   python3 powerline_setup()
   python3 del powerline_setup
   set laststatus=2 " Always display the statusline in all windows
   set showtabline=2 " Always display the tabline, even if there is only one tab
   set noshowmode " Hide the default mode text (e.g. -- INSERT -- below the statusline)
   set t_Co=256
{% endhighlight %}

## Daemon
Untuk mendapatkan perubahan di butuhkan untuk me`reload` daemon `Powerline`:
{% highlight bash %}                                                                                                                                
   powerline-daemon --replace
{% endhighlight %}


## Referensi
   * [Poweline](https://github.com/powerline/powerline)
   * [Tmux](https://github.com/tmux/tmux/wiki)
   * [Vim](https://github.com/vim)

Sekian tutorial cara install powerline di `Fedora 28`.
