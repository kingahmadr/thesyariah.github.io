---
layout:     post 
title:      "Mass Rotate Using imagemagick"
subtitle:   "imagemagick, Linux Blog"
date:       2022-07-09
author:     "ahmadcloud"
URL: "/mass-rotate-imagemagick/"
image:      "https://storage.googleapis.com/ahmadcloud-bucket/tree-736885-480.jpg"
---

## INTRODUCTION
Linux memiliki cara yang _convenient_ untuk melakukan pekerjaan repetitif.
Kita akan memanfaatkan _bash scripting languange_ untuk membuat pekerjaan repetitif lebih singkat.

Fungsi yang akan kita gunakan adalah fungi _while loop_ dan _for loop_.
Studi kasusnya adalah melakukan _renaming_ pada _multiple files_ dan juga melakukan rotasi pada _multiple file_.

## STEPS
1. Masuk ke directory file:
	> cd '[path to your directory]'
2. List file dan sort file-file tersebut menggunakan perintah berikut:
	> ls | sort

	Output setelah di-listing kurang lebih seperti berikut:
![border-resize-left-margin](/img/mass-rotate/Image1.png)

3. Kita lakukan mass rename file memanfaatkan *while loop* pada bash. Kita dapat menggunakan *one line command* pada terminal seperti berikut:

	> $ x=1

	> ls | sort | while read line;do echo "renaming file $line to $x.jpg"; mv -- "$line" $x.jpg;x=$((x+1));sleep 1;done

	Penjelasan *command*:

	**x=1:** definisi variable *x=1* pada bash session

	**ls | sort:** melakukan *listing* pada file kemudian *pipeline* ke *command sort* agar *output* file diurutkan

	**while read line:** start command untuk membaca input line by line

	**do echo "renaming file $line to $x.jpg:"** print output ke terminal
	
	**mv -- "$line" $x.jpg;x=$((x+1));sleep 1:** command untuk rename file secara masal

	**done:** penutup untuk perulangan *while loop*

	Setelah command dijalankan kurang lebih akan seperti berikut:
![border-resize-left-margin](/img/mass-rotate/Image2.png)
![border-resize-left-margin](/img/mass-rotate/Image3.png)	

4. Setelah file di-rename, kita dapat dengan mudah menerapkan perulangan berdasarkan urutan file menggunakan *for loop*.
kita akan menggunakan *for loop* untuk menerapkan rotasi masal pada beberapa gambar.

	kondisi awal sebelum dilakukan mass rotate
![border-resize-width-2](/img/mass-rotate/Image4.png)

	Kita akan melakukan rotasi agar posisi gambar sebagai berikut.
![border-resize-width](/img/mass-rotate/Image5.png)

	Sebelum melakukan rotasi kita harus melakukan instalasi package imagemagick pada machine Anda.
	
	> $ sudo apt-get install imagemagick
	
	Apabila Anda telah melakukan instalasi package tersebut, maka akan muncul output berikut ketika Anda mencoba execute command di atas.
![border-resize-width](/img/mass-rotate/Image6.png)

5. Kita akan melakukan rotasi 270 derajat untuk gambar 1-12.jpg dan 18-31.jpg. berikut contoh perintah yang dapat dijalankan:

	> $ for i in {1..10}.jpg {18..31}.jpg; do echo "rotating picture $i"; convert -rotate 270 $i $i;sleep 1;done

	Penjelasan:

	**for i in {1..10}.jpg {18..31}.jpg:** perulang terurut dengan gambar 1-10.jpg dan 18-31.jpg sebagai parameter input variabel **i**

	**do echo "rotating picture $i":** print contoh output ke terminal

	**convert -rotate 270 $i $i;sleep 1:** melakukan rotasi dengan jeda 1 detik setiap action rotasinya

	**done:** penutup untuk perulangan *for loop*

	Hasilnya kurang lebih seperti berikut ini
![border-resize-width-2](/img/mass-rotate/Image7.png)

## CONCLUSION

Penerapan looping pada tugas-tugas yang repetitif sangat mudah diterapkan pada bash di linux, bukan? :D
