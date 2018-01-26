ssh merupakan aplikasi shell yang digunakan untuk membuat koneksi terenkripsi antar sistem sehingga koneksi menjadi lebih aman. SSH sendiri terdiri dari dua aplikasi berbeda yaitu aplikasi klien ssh dan aplikasi server sshd. Pada kebanyakan distro linux biasanya sudah menyertakan aplikasi klien SSH yang di sebut ssh-clients, namun aplikasi server sshd belum di sertakan. Aplikasi server sshd di butuhkan jika host atau komputer tersebut ingin dapat dihubungi oleh ssh klien, Berikut tutorial Instalasi dan Konfigurasi SSH di Centos 7.


## instalasi
Untuk melakukan Instalasi dan Konfigurasi SSH di Centos 7, cukup jalankan perintah berikut:
{% highlight python %}
yum -y install openssh-server openssh-clients
{% endhighlight %}


## Konfigurasi sshd
Aplikasi server sshd memiliki berkas konfigurasi utama sshd_config yang tersimpan di dalam direktori /etc/ssh. Secara default aplikasi server sshd sudah bisa digukana tanpa perlu di konfigurasi. Namun demi alasan keamanan, disarankan untuk memodifikasi beberapa direktif berikut:
{% highlight python %}
Port 22 
PermitRootLogin no
{% endhighlight %}


Hal pertama yang harus dirubah adalah membatasi akses root untuk login melalui SSH. Di beberapa distro linux secara default root di ijinkan untuk login, sesuatu yang tentu sangat berbahaya. Hal ini disebabkan ketikan terjadi Brute Force para hacker tidak perlu menebak nama user yang terdapat di sistem, tetapi cukup menggunakan pengguna root untuk mencoba masuk ke sistem.


Dengan menonaktifkan akses root, berarti akan mempersulit kerja hacker karena selain sandi, root untuk login melalui SSH. Akses root dikendalikan oleh direktif `PermitRootLogin` Untuk menonaktifkan akses root cukup merubah nilai direktif tersebut menjadi `no`.


Direktif `port` juga dapat digunakan untuk menambah keamanan koneksi SSH. Kita dapat mengubah nya menjadi port berapapun selama port tersebut tidak digunakan oleh service/daemon lain.


## Konfigurasi ssh
sama halnya dengan konfigurasi sshd, ssh secara default juga dapat langsung digunakan dan tidak perlu dirubah. Namun berikut adalah beberapa direktif yang perlu di perhatikan.

{% highlight python %}
CheckHostIP yes
StrickHostKeyChecking Yes
{% endhighlight %}


Direktif `CheckHostIP` akan memaksa openSSH untuk memeriksa apakah alamat IP host terkena serangan DNS spoofing atau tidak. Direktif `StrickHostKeyChecking` ask akan memaksa OpenSSH menanyakan apakah kunci publik akan di masukkan ke berkas known_host ketika koneksi pertama kali di lakukan.


## Membuat kunci SSH
OpenSSH menyediakan perkakas untuk membuat pasangan kunci publik dan pribadi, yaitu ssh-keygen. Berikut ini kita akan membuat kunci SSH dengan user `test`.
{% highlight python %}
[test@ssh ~]$ ssh-keygen -t rsa
{% endhighlight %}


perintah di atas akan membuat pasangan kunci publik dan pribadi yang akan di simpan di direktory pengguna yang menjalankan perintah tersebut. Jika yang menjalankan perintah tersebut adalah `root` maka kunci akan di simpan di direktory `/root/.ssh`. jika yang menjalankan adalah user biasa maka kunci publik dan pribadi akan di simpan di direktori home pengguna tersebut, dalam hal ini kunci publik dan pribadi akan di simpan di folder home `test` yaitu `/home/test`.


{% highlight python %}
Generating public/private rsa key pair.
Enter file in which to save the key (/home/test/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/test/.ssh/id_rsa.
Your public key has been saved in /home/test/.ssh/id_rsa.pub.
The key fingerprint is:
4a:dd:0a:c6:35:4e:3f:ed:27:38:8c:74:44:4d:93:67 test@a
The key's randomart image is:
+--[ RSA 2048]----+
|          .oo.   |
|         .  o.E  |
|        + .  o   |
|     . = = .     |
|      = S = .    |
|     o + = +     |
|      . o + o .  |
|           . o   |
|                 |
+-----------------+
{% endhighlight %}


Jawab semua pertanyaan tersebut dengan nilai yang di inginkan atau dapat juga menggunakan nilai default dengan menekan langsung tombol `[ENTER]`. Yang perlu di pertimbangkan adalah apakan akan menggunakan passphrase atau tidak, jika `passphrase` digunakan maka passphrase akan di tanyakan setiap kali kunci pribadi digunakan untuk melakukan verifikasi kunci publik. Passphrase dapat tidak digunakan yang tentu saja akan mengurangi keamanan kunci, tetapi akan memudahkan proses `cron` ataupun `shell script` untuk menggukan OpenSSH.


## ssh-client
Aplikasi klien ssh digunakan untuk menghubungi server SSH Untuk melakukan koneksi dengan sistem lain, jalan perintah berikut:
{% highlight python %}
 [test@ssh ~]$ ssh admin@example.com
{% endhighlight %}


perintah di atas akan melakukan koneksi ke server `example.com` dengan nama pengguna `admin`. Jika baru pertama kali melakukan koneksi ke server `example.com`, maka akan muncul dialog untuk menyimpan kunci public dari server `example.com`. Untuk dapat melakukan koneksi ke server tersebut, kita harus menjawab pertanyaan tersebut dengan `yes` karena jika kita menjawab `no` maka koneksi ke server example.com akan segera di putus.


>Catatan
>
>ssh menyimpan kunci publik dari server yang pernah di hubungi ke dalam berkas .ssh/known_hosts.
>
>ssh akan memberikan peringatan jika kunci yang disimpannya dan yang diterimanya tidak sama.


## Otentikasi Kunci Publik
Otentikasi kunci publik hanya mengandalkan verifikasi pasangan kunci publik dan kunci pribadi dari sistem yang terhubung. Sebelum nya kita telah membuat kunci publik dan pribadi milik user `test`, yang dimana file `/home/test/.ssh/id_rsa.pub` adalah kunci publik dan `/home/test/.ssh/id_rsa` adalah kunci pribadi kita.


Untuk melakukan koneksi ke server jauh menggunakan kunci publik yang telah kita buat tadi, syarat nya dalah kunci publik kita harus terdaftar pada file `authorized_keys` milik server jauh. jalankan perintah berikut untuk mengimport kunci publik kita ke file `authorized_keys` milik server jauh.


{% highlight python %}
cat /home/test/.ssh/id_rsa.pub | ssh admin@example.com "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
{% endhighlight %}


## sumber
[www.nusa.id](https://www.nusa.id/)
