# Excalidraw with Cloudflare Tunnel

A Docker Compose setup for Excalidraw with Cloudflare Tunnel integration for secure remote access via `draw.homiecule.love`.

## Setup Instructions

### 1. Cloudflare Tunnel Configuration

1. Go to [Cloudflare Zero Trust Dashboard](https://one.dash.cloudflare.com/)
2. Navigate to **Zero Trust > Access > Tunnels**
3. Create a new tunnel or use an existing one
4. Configure the tunnel with the following settings:
   - **Hostname**: `draw.homiecule.love`
   - **Service**: `http://nginx:80`
5. Copy the tunnel token

### 2. Environment Configuration

1. Copy the environment template:
   ```powershell
   Copy-Item .env.example .env
   ```

2. Edit the `.env` file and replace `your_tunnel_token_here` with your actual Cloudflare tunnel token

### 3. Deploy the Application

1. Start the services:
   ```powershell
   docker-compose up -d
   ```

2. Check the status:
   ```powershell
   docker-compose ps
   ```

### 4. Access Your Application

- Your Excalidraw instance will be available at: `https://draw.homiecule.love`
- The tunnel automatically handles SSL/TLS termination through Cloudflare

## Architecture

- **excalidraw**: Main Excalidraw application
- **excalidraw-storage-backend**: Handles drawing persistence
- **excalidraw-room**: Manages real-time collaboration via WebSockets
- **redis**: Caching and session storage
- **nginx**: Reverse proxy and load balancer
- **cloudflared**: Cloudflare tunnel client for secure remote access

## Monitoring

Check logs for any service:
```powershell
docker-compose logs -f [service_name]
```

Available services: `excalidraw`, `excalidraw-storage-backend`, `excalidraw-room`, `redis`, `nginx`, `cloudflared`

## Troubleshooting

### Tunnel Issues
- Verify your tunnel token is correct in the `.env` file
- Check that the tunnel is active in the Cloudflare dashboard
- Ensure the tunnel is configured to point to `http://nginx:80`

### Application Issues
- Check that all containers are running: `docker-compose ps`
- Review nginx logs: `docker-compose logs nginx`
- Verify network connectivity between containers
