

CASE1     <br/>

**1.1 Sanal makinada bir Centos kurup, güncellemelerin yapılması** <br/>
 [VirtualBox](https://www.virtualbox.org/wiki/Downloads)    <br/>
 [CentOS-7](http://isoredirect.centos.org/centos/7/isos/x86_64/CentOS-7-x86_64-Minimal-1708.iso)
 
**1.2 Kişisel bir user yaratıyoruz**

**1.3 Sunucuya 2.disk olarak 10GB disk eklenmesi ve "bootcamp" olarak mount edilmesi** <br/>
Virtual box'da manuel olarak diski ekliyoruz. <br/>
`lsblk`    <br/> 
Eklediğimiz diski görebiliriz.  <br/>
`sudo fdisk /dev/sdb`  <br/>  
 `n` <br/>
 +9G <br/>
Böylece partition eklenmiş oldu.<br/>
`sudo mkdir -p /opt/bootcamp` <br/>
`sudo mkfs.ext4  dev/sdb1 `<br/>
Partition'dan bir file system oluşturdu. Artık mount edebiliriz.  
`sudo mount /dev/sdb1 /opt/bootcamp/` <br/>
Disk mount edildi.       <br/>
Kalıcı olmasını istiyorsak;    <br/>
`sudo vi /etc/ftsab `   <br/>
`/dev/sdb1  /opt/bootcamp   ext4   defaults  0 0 `<br/>
`mount -a `<br/>
`reboot` <br/>
Artık kalıcı hale geldi.  <br/>

**1.4 /opt/bootcamp/ altında bootcamp.txt diye bir file yaratılıp, file'ın içerisine "merhaba trendyol" yazılması**  <br/>
`sudo touch bootcamp.txt /opt/bootcamp `<br/>
`sudo echo "merhaba trendyol" >> bootcamp.txt `<br/>
`sudo cat bootcamp.txt  `<br/>

**1.5 Kişisel kullanıcının home dizininde tek bir komut kullanarak bootcamp.txt file'ını bulup, bootcamp diskine taşıması** <br/>
`sudo find /home -type f -name "bootcamp.txt" -exec mv {} /opt/bootcamp`  <br/>

CASE2   <br/>
 **2.1. DB kullanan bir uygulamayı dockerized edip, nginx üzerinden serve edilmesi**  <br/>

**Kurulumlar** <br/>
Önce repository güncelleme komutlarını çalıştırıyoruz. <br/>
`sudo yum -y update`  <br/>
`sudo yum -y install epel-release` <br/>
Ansible paketini kuruyoruz.  <br/>
`sudo yum -y install ansible`  <br/>
`ansible --version`  <br/>
 `sudo cat install_docker.yml`<br/>

![image](https://user-images.githubusercontent.com/66086595/116007840-5af07280-a61a-11eb-9f75-c3be1168d7b2.png)<br/>
`ansible-playbook install_docker.yml`<br/>
Ardından docker'ın doğru bir şekilde kurulup kurulmadığını kontrol etmek için;<br/>
`systemctl status docker`<br/>
Nginx paketini kuruyoruz.<br/>
`sudo yum install nginx`<br/>
`sudo systemctl enable nginx`<br/>
