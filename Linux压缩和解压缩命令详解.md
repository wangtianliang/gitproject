#linux压缩和解压命令 zip和tar
1.把/home目录下面的mydata目录压缩为mydata.zip

    zip -r mydata.zip mydata #压缩mydata目录
2.把/home目录下面的mydata.zip解压到mydatabak目录里面

    unzip mydata.zip -d mydatabak
3.把/home目录下面的abc文件夹和123.txt压缩成为abc123.zip

    zip -r abc123.zip abc 123.txt
4.把/home目录下面的wwwroot.zip直接解压到/home目录里面

    unzip wwwroot.zip
5.把/home目录下面的abc12.zip、abc23.zip、abc34.zip同时解压到/home目录里面

    unzip abc\*.zip
6.查看把/home目录下面的wwwroot.zip里面的内容

    unzip -v wwwroot.zip
7.验证/home目录下面的wwwroot.zip是否完整

    unzip -t wwwroot.zip
8.把/home目录下面wwwroot.zip里面的所有文件解压到第一级目录

    unzip -j wwwroot.zip
9.tar基本使用
    
     tar -cf all.tar *.jpg //这条命令是将所有.jpg的文件打成一个名为all.tar的包。-c是表示产生新的包，-f指定包的文件名。
     tar -rf all.tar *.gif //这条命令是将所有.gif的文件增加到all.tar的包里面去。-r是表示增加文件的意思。 
     tar -uf all.tar logo.gif //这条命令是更新原来tar包all.tar中logo.gif文件，-u是表示更新文件的意思。 
     tar -tf all.tar //这条命令是列出all.tar包中所有文件，-t是列出文件的意思 
     tar -xf all.tar //这条命令是解出all.tar包中所有文件，-x是解开的意思

10.查看

    tar -tf aaa.tar.gz   在不解压的情况下查看压缩包的内容
11.压缩

    tar –cvf jpg.tar *.jpg //将目录里所有jpg文件打包成tar.jpg
    tar –czf jpg.tar.gz *.jpg //将目录里所有jpg文件打包成jpg.tar后，并且将其用gzip压缩，生成一个gzip压缩过的包，命名为jpg.tar.gz
    tar –cjf jpg.tar.bz2 *.jpg //将目录里所有jpg文件打包成jpg.tar后，并且将其用bzip2压缩，生成一个bzip2压缩过的包，命名为jpg.tar.bz2
    tar –cZf jpg.tar.Z *.jpg   //将目录里所有jpg文件打包成jpg.tar后，并且将其用compress压缩，生成一个umcompress压缩过的包，命名为jpg.tar.Z

12.解压

    tar –xvf file.tar //解压 tar包
    tar -xzvf file.tar.gz //解压tar.gz
    tar -xjvf file.tar.bz2   //解压 tar.bz2tar –xZvf file.tar.Z //解压tar.Z
总结

1. *.tar 用 tar –xvf 解压

2. *.gz 用 gzip -d或者gunzip 解压

3. *.tar.gz和*.tgz 用 tar –xzf 解压

4. *.bz2 用 bzip2 -d或者用bunzip2 解压

5. *.tar.bz2用tar –xjf 解压

6. *.Z 用 uncompress 解压

7. *.tar.Z 用tar –xZf 解压