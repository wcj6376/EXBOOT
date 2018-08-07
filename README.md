version=20180801
author=wcj6376 (qq:893919135)
���¹���:(����QQȺ��340132896)
����ʹ���뽫tool�µ�bash,busybox,exfunction,debian���Ƶ�/system/xbin�£�Ȩ��777;
�ٽ�debian.tar.bz2��ѹ��/data/local/debian�ļ���;ע���ļ�·����
��ѹ���mkdir -p /data/local/debian ;  cd /data/local ; busybox tar xjf /sdcard/EXBOOT/debian/debian.tar.bz2 )
����ն�su�س�,������debian�س����ɿ�ʼ���顣
�����Ubuntuͬ��

һЩ���ÿ�ݣ��������mkshrc��
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

#ѹ��
compress()
{
echo "  ��ѡĿ¼�У�"
for dir in $(ls )
do
  [ -d $dir ] && Blue $dir 
done

echo "  ��ѡ�ļ��У�"
for file in $(ls *)
do
  [ -f $file ] && Green $file 
done

echo -n "�������ļ���Ŀ¼����"
read file
[ -z $file ] && echo "����Ϊ�գ��Զ����ء�" && sleep  0.5 && exit
if [ -d $file ];then
 tar zcvf "$file".tar.gz "$file"
[ "$?"==0 ] && echo "�ļ�ѹ���ɹ�����鿴��" && ls $file.tar.gz || exit
elif [ -f $file ];then
echo -n "������ѹ�����ļ����ͣ�"
read type
[ -z $type ] && echo "����Ϊ��,�Զ����ء�" && sleep 0.5 && exit
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
*) echo "�ݲ�֧��ѹ��$type���ͣ�" 
;;
esac
[ "$?"==0 ] && echo "�ļ�ѹ���ɹ�����鿴��" && ls *.$type || exit
else
echo "��Ŀ¼���޴��ļ���"
fi
sleep 2
}

#��ѹ
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
        *)     echo "$1���ܽ�ѹ";; 
         esac 
     else 
         echo "$1�ļ�������"; 
     fi 
}
