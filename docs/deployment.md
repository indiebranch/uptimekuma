# Deployment

1. SSH into the server.
2. Navigate to the deployment directory: `cd ~/uptimekuma`
3. Start the services: `docker compose up -d`
4. Check if the container is running: `docker compose ps`
5. Check container logs: `docker compose logs uptime-kuma`

## Troubleshooting

If the service is not accessible via IP address and port:

### 1. Verify Container is Running
```bash
docker compose ps
```
The container should show as "Up" status.

### 2. Check Container Logs
```bash
docker compose logs uptime-kuma
```
Look for any error messages.

### 3. Verify Port Binding
```bash
docker compose ps
# or
docker ps
# or check port binding directly
ss -tlnp | grep 3001
# or
netstat -tlnp | grep 3001
```

### 4. Check Firewall
If using UFW (Ubuntu/Debian):
```bash
sudo ufw status
sudo ufw allow 3001/tcp
```

If using firewalld (CentOS/RHEL):
```bash
sudo firewall-cmd --list-ports
sudo firewall-cmd --permanent --add-port=3001/tcp
sudo firewall-cmd --reload
```

### 5. Verify Docker Network
```bash
docker network ls
docker network inspect uptimekuma_default
```

### 6. Test Local Connection
From the server itself:
```bash
curl http://localhost:3001
# or
curl http://127.0.0.1:3001
```

### 7. Check if Port is Listening
```bash
sudo lsof -i :3001
# or
sudo ss -tlnp | grep 3001
```

### 8. Restart Services
```bash
docker compose down
docker compose up -d
```

### 9. Check Server IP
Make sure you're using the correct IP address:
```bash
ip addr show
# or
hostname -I
```

## Access
Once running, access UptimeKuma at: `http://YOUR_SERVER_IP:3001`