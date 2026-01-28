# Freeinternetforiran
Conduit: High-Performance Proxy Tunnel for Iran

۳. بخش آموزش نصب (Installation)


مرحله اول: دانلود و آماده‌سازی

sudo apt update && sudo apt install -y curl ipset iptables-persistent
cd /opt

sudo curl -L -o conduit https://github.com/ssmirr/conduit/releases/download/87cc1a3/conduit-linux-amd64

sudo chmod +x conduit

مرحله دوم: امنیت و محدودسازی به ایران ( برای کاربران ایرانی)
 با این کار امنیت سرور تضمین می‌شود:


# ایجاد لیست سفید ایران
sudo ipset create iran_ips hash:net maxelem 100000

curl -s https://www.ipdeny.com/ipblocks/data/countries/ir.zone | xargs -I {} sudo ipset add iran_ips {}

# تنظیم فایروال
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

sudo iptables -A INPUT -p tcp --dport 1080 -m set --match-set iran_ips src -j ACCEPT

sudo iptables -A INPUT -p tcp --dport 1080 -j DROP
مرحله سوم: اجرا

./conduit start -v -b 10 -m 100
