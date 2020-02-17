mv /usr/sbin/opal-prd /usr/sbin/opal-prd.ori
cp ./opal-prd /usr/sbin/opal-prd
chmod u+rx /usr/sbin/opal-prd
systemctl stop tuned
systemctl restart opal-prd
opal-prd -e occ overclock-mode
cpupower -c all frequency-set -f 3.5G
cpupower -c all frequency-info|grep 'current CPU frequency'|sort|uniq -c

#opal-prd -e occ nominal-mode
#cpupower -c all frequency-set -g ondemand

