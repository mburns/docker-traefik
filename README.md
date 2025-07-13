# Docker Traefik Stack

A comprehensive Docker Compose stack for self-hosted services with Traefik as a reverse proxy, featuring media management, monitoring, security, and development tools.

## 🚀 Features

- **Reverse Proxy**: Traefik with automatic SSL certificates via Cloudflare DNS
- **Media Management**: Plex, Sonarr, Radarr, Lidarr, Readarr, and more
- **Download Management**: SABnzbd, qBittorrent, Transmission, JDownloader
- **Monitoring**: Grafana, Prometheus, InfluxDB, Netdata
- **Security**: Authelia, CrowdSec, Fail2Ban, Vault
- **Development**: VSCode, Homepage dashboard
- **Network**: WireGuard, ZeroTier, I2P, IPFS
- **Tools**: File management, RSS feeds, search engines

## 📋 Prerequisites

- Docker and Docker Compose installed
- A domain name with Cloudflare DNS
- Cloudflare API token with DNS edit permissions
- Linux server with sufficient resources

## 🛠️ Quick Start

> **New to Docker Traefik Stack?** Check out the [Getting Started Guide](GETTING_STARTED.md) for a step-by-step walkthrough.

### Option 1: Automated Setup (Recommended for New Users)

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd docker-traefik
   ```

2. **Run the configuration wizard:**
   ```bash
   ./scripts/config-wizard.sh
   ```

3. **Run the quick start script:**
   ```bash
   ./scripts/quick-start.sh
   ```

### Option 2: Manual Setup

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd docker-traefik
   ```

2. **Copy and configure environment variables:**
   ```bash
   cp .env.example .env
   nano .env
   ```

3. **Create required directories:**
   ```bash
   sudo mkdir -p /opt/docker/{appdata,logs,secrets}
   sudo mkdir -p /data/{Movies,TV,Music,Books,Downloads}
   sudo chown -R $USER:$USER /opt/docker /data
   ```

4. **Create secrets:**
   ```bash
   # Create secret files
   echo "your-cloudflare-email" > /opt/docker/secrets/cf_email
   echo "your-cloudflare-api-key" > /opt/docker/secrets/cf_api_key
   echo "your-htpasswd-hash" > /opt/docker/secrets/htpasswd
   echo "your-traefik-forward-auth-config" > /opt/docker/secrets/traefik_forward_auth
   ```

5. **Start core services:**
   ```bash
   docker-compose --profile core up -d
   ```

6. **Start additional services:**
   ```bash
   # Media services
   docker-compose --profile media up -d
   
   # All services
   docker-compose --profile all up -d
   ```

## 📁 Service Profiles

- **core**: Essential services (Traefik, OAuth, Socket Proxy)
- **apps**: Web applications and tools
- **media**: Media management services
- **arrs**: *Arr services (Sonarr, Radarr, etc.)
- **downloads**: Download managers
- **monitoring**: Monitoring and metrics
- **security**: Security services
- **web**: Web browsers and development tools
- **all**: All services

## 🎛️ Service Management

### Management Scripts

Use these scripts for easy service management:

```bash
# Service management
./scripts/manage-services.sh help
./scripts/manage-services.sh start core
./scripts/manage-services.sh status all
./scripts/manage-services.sh logs traefik
./scripts/manage-services.sh update all

# Status dashboard
./scripts/status-dashboard.sh
./scripts/status-dashboard.sh -p core
./scripts/status-dashboard.sh -l traefik

# Configuration wizard
./scripts/config-wizard.sh

# Quick start
./scripts/quick-start.sh
```

### Quick Commands

```bash
# Check status
./scripts/status-dashboard.sh

# Start core services
./scripts/manage-services.sh start core

# View logs
./scripts/manage-services.sh logs [service]

# Update all services
./scripts/manage-services.sh update all

# Create backup
./scripts/manage-services.sh backup

# Run health check
./scripts/manage-services.sh health

# Clean up
./scripts/manage-services.sh clean
```

## 🔧 Configuration

### Environment Variables

Key environment variables to configure:

- `DOMAINNAME_CLOUD_SERVER`: Your domain name
- `CLOUDFLARE_EMAIL`: Cloudflare account email
- `CLOUDFLARE_IPS`: Cloudflare IP ranges
- `PUID/PGID`: User/group IDs for file permissions
- `TZ`: Timezone

### Networks

- `t2_proxy`: Main network for services behind Traefik
- `socket_proxy`: Network for Docker socket access
- `default`: Default bridge network

### Volumes

- `/opt/docker/appdata`: Application data
- `/opt/docker/logs`: Log files
- `/data`: Media and data storage
- `/downloads`: Download directory

## 🔒 Security

### Authentication

- **OAuth**: Google OAuth via Traefik Forward Auth
- **Authelia**: Multi-factor authentication
- **CrowdSec**: Intrusion detection and prevention

### SSL/TLS

- Automatic SSL certificates via Let's Encrypt
- Cloudflare DNS challenge for wildcard certificates
- HSTS and security headers

### Network Security

- Docker socket proxy for secure container access
- Network isolation between services
- Firewall rules and rate limiting

## 📊 Monitoring

### Metrics Collection

- **Prometheus**: Metrics collection
- **InfluxDB**: Time-series database
- **Grafana**: Dashboards and visualization
- **Netdata**: Real-time system monitoring

### Logging

- Centralized logging with Loki
- Log rotation and retention
- Structured logging with JSON format

## 🚨 Troubleshooting

### Common Issues

1. **SSL Certificate Issues**
   - Verify Cloudflare API credentials
   - Check DNS records are properly configured
   - Ensure domain is proxied through Cloudflare

2. **Permission Issues**
   - Verify PUID/PGID match your user
   - Check directory permissions
   - Ensure Docker socket access

3. **Network Issues**
   - Verify network configuration
   - Check firewall rules
   - Ensure ports are not conflicting

### Debug Commands

```bash
# Check service status
docker-compose ps

# View logs
docker-compose logs -f [service-name]

# Check Traefik configuration
docker-compose exec traefik traefik version

# Test network connectivity
docker-compose exec [service] ping [target]
```

## 📈 Performance Optimization

### Resource Limits

Services have resource limits configured:
- CPU: 0.25-2.0 cores per service
- Memory: 256M-2G per service
- Storage: Appropriate volume mounts

### Scaling

- Use Docker Compose profiles to run only needed services
- Monitor resource usage with Grafana dashboards
- Adjust resource limits based on hardware capabilities

## 🔄 Updates

### Automatic Updates

Watchtower automatically updates containers:
- Scheduled updates at 2 AM daily
- Cleanup of old images and volumes
- Notification support via Shoutrrr

### Manual Updates

```bash
# Update specific service
docker-compose pull [service-name]
docker-compose up -d [service-name]

# Update all services
docker-compose pull
docker-compose up -d
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- [Traefik](https://traefik.io/) for the reverse proxy
- [LinuxServer.io](https://www.linuxserver.io/) for container images
- [Homepage](https://github.com/benphelps/homepage) for the dashboard
- All the open-source projects that make this stack possible

## 📞 Support

For support and questions:
- Check the troubleshooting section
- Review service-specific documentation
- Open an issue on GitHub
- Join our community discussions