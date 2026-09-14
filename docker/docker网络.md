# host网络
就是宿主机网络，容器占用的端口不用映射，会直接占用宿主机的端口，



# bridge 网络
- 虚拟网卡，单独子网，一般虚拟网卡的网关(172.16.0.1)就表示的是宿主机
- 容器访问宿主机，就访问子网网关或者是宿主机的ip地址
- 从子网到宿主机的网络，会经过防火墙（ufw）所以需要开放端口







services:
  tailscale:
    image: tailscale/tailscale:latest
    container_name: tailscale
    network_mode: host                # 使用 host 模式共享 WSL 网络
    privileged: true                  # 给予特权以创建 TUN 虚拟网卡
    volumes:
      - ./tailscale_state:/var/lib/tailscale  # 持久化保存密钥和登录状态
      - /dev/net/tun:/dev/net/tun             # 映射网卡驱动核心
    environment:
      - TS_USERSPACE=false
      - TS_STATE_DIR=/var/lib/tailscale # 持久化登录状态，在挂载卷里可以看到state文件
    restart: unless-stopped









