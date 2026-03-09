# Mission Control - CasaOS Installation

This guide covers installing Mission Control on CasaOS.

## Quick Installation

1. Open CasaOS App Store
2. Click "Import" or "Custom Install"
3. Use this docker-compose file: `docker-compose.casaos.yml`

Or use the command line:

```bash
docker-compose -f docker-compose.casaos.yml up -d
```

## Configuration

The CasaOS installation uses the following default settings:

- **Port**: 3000 (web interface)
- **Default Username**: admin
- **Default Password**: changeme (⚠️ **CHANGE THIS!**)
- **API Key**: changeme (⚠️ **CHANGE THIS!**)

### Environment Variables

You can configure these through CasaOS UI or by editing the docker-compose.casaos.yml:

- `PORT`: Web interface port (default: 3000)
- `NODE_ENV`: Environment mode (default: production)
- `AUTH_USER`: Initial admin username
- `AUTH_PASS`: Initial admin password
- `API_KEY`: API key for headless access

See [.env.example](.env.example) for the complete list of available environment variables.

## Data Persistence

Mission Control data is stored in `/DATA/AppData/mission-control/data` which is mounted to `/app/.data` inside the container.

## Security Considerations

⚠️ **IMPORTANT**:

1. **Change default credentials immediately** after first login
2. **Set strong passwords** for `AUTH_PASS` and `API_KEY`
3. **Deploy behind a reverse proxy with TLS** for network-accessible deployments
4. Review [SECURITY.md](SECURITY.md) for the vulnerability reporting process

## Accessing Mission Control

After installation, access Mission Control at:

```
http://your-casaos-ip:3000
```

Login with:
- Username: `admin` (or your configured AUTH_USER)
- Password: `changeme` (or your configured AUTH_PASS)

## Supported Architectures

- amd64
- arm64
- arm (v7)

## Updating

To update to the latest version:

1. Pull the latest image:
   ```bash
   docker pull ghcr.io/vinayakv22/mission-control:latest
   ```

2. Restart the container:
   ```bash
   docker-compose -f docker-compose.casaos.yml up -d
   ```

## Troubleshooting

### Container won't start

Check logs:
```bash
docker logs mission-control
```

### Can't access web interface

1. Verify the container is running: `docker ps`
2. Check port mapping is correct
3. Ensure firewall allows port 3000

### Database issues

The SQLite database is stored in `/DATA/AppData/mission-control/data/`. If you experience database corruption, you may need to restore from a backup or remove the data directory to start fresh.

## Support

- Documentation: [README.md](README.md)
- Issues: [GitHub Issues](https://github.com/vinayakv22/mission-control/issues)
- Security: [SECURITY.md](SECURITY.md)

## License

[MIT](LICENSE) © 2026 Builderz Labs
