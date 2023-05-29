# Nginx_web 
yum install cyrus-sasl cyrus-sasl-gssapi cyrus-sasl-plain krb5-libs libcurl net-snmp openldap openssl xz-libs -y
vi /etc/yum.repos.d/nginx.repo
yum install nginx -y

# create ssl local
sudo mkdir /smb
sudo openssl req -x509 -nodes -days 3650 -newkey rsa:2048 -keyout /smb/prod.key -out /smb/prod.crt

# edit file config
vi /usr/lib/systemd/system/nginx.service
vi /etc/nginx/nginx.conf
# open port
firewall-cmd --zone=public --add-port=80/tcp --permanent
firewall-cmd --zone=public --add-port=443/tcp --permanent
firewall-cmd --reload

# check status service
systemctl daemon-reload
systemctl restart nginx.service
systemctl enable nginx.service
