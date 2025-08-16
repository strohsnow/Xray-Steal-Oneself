### Install Docker
```
sudo curl -fsSL https://get.docker.com | sh
```

### Enable TCP BBR
```
echo -e "net.core.default_qdisc = fq\nnet.ipv4.tcp_congestion_control = bbr" | sudo tee /etc/sysctl.d/99-bbr.conf > /dev/null && sudo sysctl -p /etc/sysctl.d/99-bbr.conf
```

### Configure log rotation
Create a directory for logs:
```
mkdir -p /var/log/xray
```
Install logrotate:
```
sudo apt update && sudo apt install logrotate
```
Create a logrotate configuration file:
```
sudo nano /etc/logrotate.d/xray
```
Paste the following logrotate configuration for Xray:
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
