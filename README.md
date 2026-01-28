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

⚡ مقیاس‌پذیری و ظرفیت بالا
یکی از بزرگترین مزایای Conduit، توانایی مدیریت تعداد بالای کاربران همزمان است. شما می‌توانید با توجه به قدرت سرور خود (CPU و RAM)، ظرفیت را تا ۱۰۰۰ کاربر یا بیشتر افزایش دهید.

پشتیبانی از ۱۰۰۰+ کاربر: با تغییر مقدار -m می‌توانید محدودیت ۲۰۰ کاربر پیش‌فرض را به ۱۰۰۰ یا بیشتر تغییر دهید.

مدیریت پهنای باند: برای اینکه سرور به اشباع نرود، می‌توانید پهنای باند هر کاربر را روی اعداد پایین‌تر (مثلاً ۲ یا ۵ مگابیت) ست کنید.

دستور پیشنهادی برای ۱۰۰۰ کاربر:



./conduit start -v -b 2 -m 1000

![ce5eb6b8-2909-4fec-996c-33f4b5de5ebb](https://github.com/user-attachments/assets/8b725c87-8d91-479e-8bcb-a0a571d7f2c9)
