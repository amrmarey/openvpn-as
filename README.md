
# 🚀 OpenVPN-AS Docker Compose Deployment

This repository provides a complete setup for deploying [OpenVPN Access Server (OpenVPN-AS)](https://openvpn.net/access-server/) using Docker Compose. 
It features **dedicated volumes, networks**, and a **health check mechanism** for ensuring service availability. 

---

## 🌟 Features

- 🐳 **Docker Compose-based Deployment**: Simplifies container management with a declarative configuration.
- 📂 **Dedicated Volume**: Persistent storage for OpenVPN-AS data.
- 🔒 **Dedicated Network**: Isolates the service in a private bridge network.
- ✅ **Health Check**: Monitors service availability on port `943` (Admin and Web UI).
- 🔄 **Automatic Restarts**: Ensures the container always restarts on failure.

---

## 🔧 Prerequisites

1. **Docker** (20.10+ recommended)
2. **Docker Compose** (v2.0+ recommended)

---

## 🚀 Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/amrmarey/openvpn-as.git
cd openvpn-as
```

### 2. Customize the Configuration

- Open `docker-compose.yml`.
- Update the `volumes` and `networks` sections if necessary.

### 3. Deploy the Service
Run the following command to start the OpenVPN-AS container:
```bash
docker-compose up -d
```

---

## ⚙️ Configuration Details

### Docker Compose File

The `docker-compose.yml` includes:
- **Ports**: 
  - `943`: Admin and Web UI
  - `443`: HTTPS for VPN
  - `1194/udp`: VPN traffic
- **Volume**: 
  - Mounts OpenVPN-AS data to the `openvpn-data` volume for persistence.
- **Network**:
  - Isolates the service using the `openvpn-net` network.
- **Health Check**:
  - Validates service health via HTTP on `localhost:943`.

### Environment Variables
Refer to the [OpenVPN-AS Docker documentation](https://hub.docker.com/r/openvpn/openvpn-as) for available configuration options.

---

## 🔍 Health Check

The service includes a health check to monitor the Admin Web UI on port `943`. Docker periodically tests service availability:
```yaml
healthcheck:
  test: ["CMD", "curl", "-f", "http://localhost:943/"]
  interval: 30s
  timeout: 10s
  retries: 3
  start_period: 10s
```

---

## 🛠️ Managing the Service

### Check the Logs
```bash
docker-compose logs -f
```

### Stop the Service
```bash
docker-compose down
```

### Monitor Health
```bash
docker ps
```
Look for `(healthy)` in the `STATUS` column.

---

## ❓ Troubleshooting

1. **Port Conflicts**: 
   - Ensure `943`, `443`, and `1194` are not in use by other services.
2. **Permission Issues**: 
   - Verify Docker has the correct permissions to manage volumes and networks.

---

## 🤝 Contributing

Contributions are welcome!

- Submit issues or pull requests to enhance this project.
- Reach out at 📧 **amr.marey@msn.com**.

---

## 📜 License

This repository is licensed under the [MIT License](LICENSE).

---

## 📚 References

- [OpenVPN Access Server Documentation](https://openvpn.net/access-server/)
- [Docker Hub: OpenVPN-AS](https://hub.docker.com/r/openvpn/openvpn-as)
