* **下载hack过的[opal-prd](https://raw.githubusercontent.com/junlizhang/PowerLinux/master/fix-freq/opal-prd)二进制文件**
```
wget https://raw.githubusercontent.com/junlizhang/PowerLinux/master/fix-freq/opal-prd -O /root/opal-prd
chmod u+rx /root/opal-prd
```
* **确保系统中opal-prd服务已经开启**
``systemctl restart opal-prd``
* **用hack过的opal-prd将处理器设置为超频模式**
``/root/opal-prd -e occ overclock-mode``
* **设置固定主频如3.5G赫兹**
``cpupower -c all frequency-set -f 3.5G``
* **查询CPU主频**
``cpupower -c all frequency-info|grep 'current CPU frequency'|sort|uniq -c``
* **通过如下命令复原处理器主频配置**
```
opal-prd -e occ nominal-mode
cpupower -c all frequency-set -g ondemand
```
