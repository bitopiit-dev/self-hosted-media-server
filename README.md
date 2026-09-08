# Self-Hosted Media Streaming Server (Jellyfin & Tailscale Funnel)

An enterprise-inspired, secure personal media streaming platform deployed on local hardware with zero-trust public HTTPS ingress via Tailscale Funnel.

---

## 📌 Architecture Overview

This project showcases a private media server environment designed to provide high-performance on-premise playback across the local area network while securely routing remote traffic over the public internet without port forwarding or exposing router ports.

```text
                  +-----------------------------------+
                  |         Remote Web Clients        |
                  |     (Browsers / Mobile Apps)      |
                  +-----------------+-----------------+
                                    |
                                    | HTTPS (Port 443)
                                    v
                  +-----------------------------------+
                  |    Tailscale Funnel (Ingress)     |
                  |  - Let's Encrypt TLS Automation   |
                  |  - Public DNS Management          |
                  +-----------------+-----------------+
                                    |
                                    | Reverse Proxy
                                    v
  +---------------------------------------------------------------+
  | Host Workstation (Windows 11)                                 |
  |                                                               |
  |   +-----------------------+       +-----------------------+   |
  |   |   Tailscale Node      | ----> |    Jellyfin Server    |   |
  |   |  (Background Service) |       |     (Port 8096)       |   |
  |   +-----------------------+       +-----------+-----------+   |
  |                                               |               |
  |                                   +-----------v-----------+   |
  |                                   |  Local Media Storage  |   |
  |                                   |   (Movies, Series,    |   |
  |                                   |    Music Videos)      |   |
  |                                   +-----------------------+   |
  +---------------------------------------------------------------+
