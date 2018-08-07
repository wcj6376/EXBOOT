version=20180801
author=wcj6376 (qq:893919135)
更新功能:(反馈QQ群：340132896)
初次使用请将tool下的bash,busybox,exfunction,debian复制到/system/xbin下，权限777;
再将debian.tar.bz2解压到/data/local/debian文件夹;注意文件路径，
解压命令（mkdir -p /data/local/debian ;  cd /data/local ; busybox tar xjf /sdcard/EXBOOT/debian/debian.tar.bz2 )
最后终端su回车,再输入debian回车即可开始体验。
如果是Ubuntu同理。

一些常用快捷，可添加在mkshrc中
alias tar1='tar -xzvf'
alias tar2='tar -czvf'
alias ls='busybox ls'
alias l='ls'
alias la='l -a'
alias ll='l -l'
alias lo='l -al'
alias c='clear'
alias ..='cd ..'
alias ...='cd ../..'
alias jy='extract'
alias db='compress'
alias chr='chmod -R 777'
alias mt='mount -t ext4'
alias um='umount -l'
alias mc='make clean'
alias mk='make -j4'
alias mi='make install'
jtby() { gcc $1 -o $2 -static ;}
mcd() { mkdir -p $1 && cd $1;}
cls() { cd $1 && ls;}
md5check() { md5sum $1 | grep $2;}

Red () {
echo -e "\e[1;31m$@\e[0m"
}
Green () {
echo -e "\e[1;32m$@\e[0m"
}
Yellow () {
echo -e "\e[1;33m$@\e[0m"
}
Blue () {
echo -e "\e[1;34m$@\e[0m"
}

#压缩
compress()
{
echo "  可选目录有："
for dir in $(ls )
do
  [ -d $dir ] && Blue $dir 
done

echo "  可选文件有："
for file in $(ls *)
do
  [ -f $file ] && Green $file 
done

echo -n "请输入文件或目录名："
read file
[ -z $file ] && echo "输入为空，自动返回。" && sleep  0.5 && exit
if [ -d $file ];then
 tar zcvf "$file".tar.gz "$file"
[ "$?"==0 ] && echo "文件压缩成功，请查看！" && ls $file.tar.gz || exit
elif [ -f $file ];then
echo -n "请输入压缩的文件类型："
read type
[ -z $type ] && echo "输入为空,自动返回。" && sleep 0.5 && exit
case $type in
bz2|xz) tar jcvf ${file}.tar.$type $file
;;
gz)  tar zcjf ${file}.tar.$type $file
;;
rar) rar e $file.$type $file
;;
tar) tar vcf $file.$type $file
;;
zip) zip $file.$type $file
;;
Z|tgz) tar zcvf $file.tar.$type $file
;;
7Z) 7z $file.$type $file
;;
*) echo "暂不支持压缩$type类型！" 
;;
esac
[ "$?"==0 ] && echo "文件压缩成功，请查看！" && ls *.$type || exit
else
echo "该目录下无此文件！"
fi
sleep 2
}

#解压
extract() { 
    if [ -f $1 ] ; then 
      case $1 in 
        *.tar.bz2)   tar xjf $1     ;; 
        *.tar.gz)    tar xzf $1     ;; 
        *.bz2)       bunzip2 $1     ;; 
        *.rar)       unrar e $1     ;; 
        *.gz)        gunzip $1      ;; 
        *.tar)       tar xf $1      ;; 
        *.tbz2)      tar xjf $1     ;; 
        *.tgz)       tar xzf $1     ;; 
        *.zip)       unzip $1       ;; 
        *.Z)         uncompress $1  ;; 
        *.7z)        7z x $1        ;; 
        *.tar.xz)    tar vxf $1       ;;
        *.tar.lz)    lzip -d $1     ;;
        *)     echo "$1不能解压";; 
         esac 
     else 
         echo "$1文件不存在"; 
     fi 
}

exboot520.tar.bz2下载
https://www.baidupcs.com/rest/2.0/pcs/file?method=batchdownload&app_id=250528&zipcontent=%7B%22fs_id%22%3A%5B394907432994605%5D%7D&sign=DCb740ccc5511e5e8fedcff06b081203:4o9UQKA4MjT38f%2Bnr6MJN%2BFe7N0%3D&uid=302190307&time=1533736794&dp-logid=5077293989163288345&dp-callid=0&vuk=302190307
