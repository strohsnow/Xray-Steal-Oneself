### Install Docker
```
sudo curl -fsSL https://get.docker.com | sh
```

### Enable TCP BBR
```
echo -e "net.core.default_qdisc = fq\nnet.ipv4.tcp_congestion_control = bbr" | sudo tee /etc/sysctl.d/99-bbr.conf > /dev/null && sudo sysctl -p /etc/sysctl.d/99-bbr.conf
```
