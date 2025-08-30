# n8n self-hosted

## Local certificate

- Run on terminal:

  ```shell
  md ~/.n8n
  openssl req -new -newkey rsa:4096 -nodes -keyout ~/.n8n/n8n.key -out ~/.n8n/n8n.csr
  openssl x509 -req -sha256 -days 365 -in n8n.csr -signkey ~/.n8n/n8n.key -out ~/.n8n/n8n_certificate.pem
  ```

## Host on Docker

### Via Portainer

- Name: `n8n`
- Image: `docker.n8n.io/n8nio/n8n:latest`
- Port mapping:
  - host: `443`
  - container: `443`
  - `tcp`
- Volumes (Bind):
  - container: `/home/node/.n8n`
  - host `/home/your_user/.n8n`
- Network:
  - Network: `host`
  - Hostname: `raspberrypi`
- Env:
  - `TZ`, `America/Sao_Paulo`
  - `N8N_PROTOCOL`, `https`
  - `N8N_SSL_CERT`, `/home/node/.n8n/n8n_certificate.pem`
  - `N8N_SSL_KEY`, `/home/node/.n8n/n8n.key`
  - `N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS`, `false`
