# sis_2-L

sudo groupadd admin
sudo groupadd frontend
sudo groupadd backend
sudo groupadd db
sudo groupadd auditor
sudo groupadd automation

sudo mkdir -p /srv/airbooking

sudo mkdir -p /srv/airbooking/backend
sudo mkdir -p /srv/airbooking/backend/media
sudo mkdir -p /srv/airbooking/backend/logs
sudo mkdir -p /srv/airbooking/backend/config

sudo mkdir -p /srv/airbooking/frontend
sudo mkdir -p /srv/airbooking/frontend/logs

sudo mkdir -p /srv/airbooking/db/data
sudo mkdir -p /srv/airbooking/db/backups
sudo mkdir -p /srv/airbooking/db/logs

sudo mkdir -p /etc/nginx/sites-available
sudo mkdir -p /etc/nginx/sites-enabled

sudo mkdir -p /tmp/airbooking_setup
sudo mkdir -p /var/tmp/airbooking

 ls -l /srv/airbooking/

 ls -l /srv/airbooking/backend/ 
 ls -l /srv/airbooking/frontend/
 ls -l /srv/airbooking/db/

sudo chown -R backend_user:backend /srv/airbooking/backend
sudo chmod -R 750 /srv/airbooking/backend

sudo chown -R frontend_user:frontend /srv/airbooking/frontend
sudo chmod -R 750 /srv/airbooking/frontend

sudo chown -R postgres:db /srv/airbooking/db
sudo chmod -R 700 /srv/airbooking/db

sudo chown -R nginx:nginx /etc/nginx
sudo chmod -R 755 /etc/nginx

sudo useradd -m -s /bin/bash admin_user -g admin
echo "admin_user:StrongPass123" | sudo chpasswd

sudo useradd -m -s /bin/bash frontend_user -g frontend
echo "frontend_user:StrongPass123" | sudo chpasswd

sudo useradd -m -s /bin/bash backend_user -g backend
echo "backend_user:StrongPass123" | sudo chpasswd

sudo useradd -m -s /bin/bash db_user -g db
echo "db_user:StrongPass123" | sudo chpasswd

sudo useradd -m -s /bin/bash auditor_user -g auditor
echo "auditor_user:StrongPass123" | sudo chpasswd

sudo useradd -m -s /bin/bash automation_bot -g automation

sudo chown -R frontend_user:frontend /srv/airbooking/frontend
sudo chown -R backend:backend /srv/airbooking/backend
sudo chown -R db:db /srv/airbooking/db

sudo chmod -R 770 /srv/airbooking/frontend
sudo chmod -R 770 /srv/project/backend
sudo chmod -R 770 /srv/project/db

sudo visudo

admin_user ALL=(ALL:ALL) ALL
frontend_user ALL=(ALL:ALL) NOPASSWD: /bin/systemctl restart frontend.service
backend_user ALL=(ALL:ALL) NOPASSWD: /bin/systemctl restart backend.service
db_user ALL=(ALL:ALL) NOPASSWD: /usr/bin/psql


ssh-keygen -t rsa -b 4096 -C "automation@project"
ssh-copy-id automation_bot@server_ip
ssh automation_bot@server_ip
