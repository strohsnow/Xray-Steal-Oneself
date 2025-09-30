### Prerequisites
Install Docker:
```
sudo curl -fsSL https://get.docker.com | sh
```
Enable TCP BBR:
```
echo -e "net.core.default_qdisc = fq\nnet.ipv4.tcp_congestion_control = bbr" | sudo tee /etc/sysctl.d/99-bbr.conf > /dev/null && sudo sysctl -p /etc/sysctl.d/99-bbr.conf
```
Disable IPv6:
```
echo -e "net.ipv6.conf.all.disable_ipv6 = 1\nnet.ipv6.conf.default.disable_ipv6 = 1" | sudo tee /etc/sysctl.d/99-ipv6.conf > /dev/null && sudo sysctl -p /etc/sysctl.d/99-ipv6.conf
```
Install Git:
```
sudo apt update -y && sudo apt install -y git
```
Clone the repository:
```
sudo git clone https://github.com/strohsnow/Xray-Steal-Oneself /opt/Xray-Steal-Oneself
```
### Configure UFW
Disable IPv6:
```
sudo sed -i 's/^IPV6=yes/IPV6=no/' /etc/default/ufw
```
Allow SSH:
```
sudo ufw allow ssh comment "SSH"
```
Allow HTTP:
```
sudo ufw allow http comment "HTTP"
```
Allow HTTPS:
```
sudo ufw allow https comment "HTTPS"
```
Enable UFW:
```
sudo ufw enable
```
### Configure Xray
Generate uuid:
```
sudo docker run --rm ghcr.io/xtls/xray-core uuid
```
Generate x25519 key pair:
```
sudo docker run --rm ghcr.io/xtls/xray-core x25519
```
Edit values in Xray config:
```
sudo nano /opt/Xray-Steal-Oneself/xray/config.jsonc
```
Start Xray:
```
sudo docker compose -f /opt/Xray-Steal-Oneself/xray/docker-compose.yml up -d
```
### Configure Caddy
Generate a random path for sub:
```
openssl rand -hex 8
```
Copy the env file:
```
sudo cp /opt/Xray-Steal-Oneself/caddy/.env.example /opt/Xray-Steal-Oneself/caddy/.env
```
Edit values in the env file:
```
sudo nano /opt/Xray-Steal-Oneself/caddy/.env
```
Edit values in the sub file:
```
sudo nano /opt/Xray-Steal-Oneself/caddy/sub
```
Start Caddy:
```
sudo docker compose -f /opt/Xray-Steal-Oneself/caddy/docker-compose.yml up -d
```
### Configure log rotation
Install logrotate:
```
sudo apt update -y && sudo apt install -y logrotate
```
Create a logrotate configuration file:
```
sudo nano /etc/logrotate.d/xray
```
Paste the following configuration:
```
/var/log/xray/*.log {
  size 50M
  rotate 5
  compress
  missingok
  notifempty
  copytruncate
}
```
### Connect with Happ
Open Happ and import your subscription link:
```
https://your.domain.com/your_sub_path
```
