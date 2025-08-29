### Prerequisites
Install Docker:
```
sudo curl -fsSL https://get.docker.com | sh
```
Add current user to the docker group (if not root):
```
sudo usermod -aG docker $USER
```
Enable TCP BBR:
```
echo -e "net.core.default_qdisc = fq\nnet.ipv4.tcp_congestion_control = bbr" | sudo tee /etc/sysctl.d/99-bbr.conf > /dev/null && sudo sysctl -p /etc/sysctl.d/99-bbr.conf
```
Install Git:
```
sudo apt update -y && sudo apt install -y git
```
Clone the repository:
```
sudo git clone https://github.com/strohsnow/Xray-Steal-Oneself /opt/Xray-Steal-Oneself
```
### Configure Xray
Generate uuid:
```
docker run --rm ghcr.io/xtls/xray-core uuid
```
Generate x25519 key pair:
```
docker run --rm ghcr.io/xtls/xray-core x25519
```
Edit values in Xray config:
```
sudo nano /opt/Xray-Steal-Oneself/xray/config.jsonc
```
Create a directory for logs:
```
sudo mkdir -p /var/log/xray
```
Start Xray:
```
docker compose -f /opt/Xray-Steal-Oneself/xray/docker-compose.yml up -d
```
### Configure Caddy
Generate a sub path:
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
docker compose -f /opt/Xray-Steal-Oneself/caddy/docker-compose.yml up -d
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
