# IPTVnator Docker Stack für Portainer

Selbstgehosteter IPTV‑Player mit Web‑Frontend und Backend als Docker‑Stack für Portainer.  
Basierend auf [`4gray/iptvnator`](https://github.com/4gray/iptvnator) und [`4gray/iptvnator-backend`](https://github.com/4gray/iptvnator-backend). [web:1][web:2][web:11][web:14]

---

## 📦 Was ist enthalten?

- `docker-compose.yml` für Portainer (Stack‑Import)
- Klare Trennung von Frontend (Nginx) und Backend (API‑Service)
- Health checks für saubere Startup‑Reihenfolge
- Netzwerk `iptv-net` als eigenes Docker‑Bridge‑Netzwerk

---

## 🚀 Voraussetzungen

- Docker installiert
- Portainer (CE oder BP) [web:7][web:13]
- Zugriff auf Docker‑Hub (Images `4gray/iptvnator` und `4gray/iptvnator-backend`)

---

## 🧩 Portainer‑Stack einrichten

1. In Portainer:  
   **Stacks → Add stack**
2. Stack‑Name z. B. `iptvnator`
3. In den Web‑Editor kopieren oder Datei uploaden:
   ```yaml
   version: "3.8"
   services:
     iptvnator-backend:
       image: 4gray/iptvnator-backend:latest
       container_name: iptvnator-backend
       restart: unless-stopped
       ports:
         - "7333:3000"
       environment:
         - CLIENT_URL=http://192.168.178.11:4333
       healthcheck:
         test: ["CMD-SHELL", "wget -q --spider http://127.0.0.1:3000 || exit 1"]
         interval: 30s
         timeout: 10s
         retries: 5
         start_period: 20s
       networks:
         - iptv-net

     iptvnator-frontend:
       image: 4gray/iptvnator:latest
       container_name: iptvnator-frontend
       restart: unless-stopped
       ports:
         - "4333:80"
       environment:
         - BACKEND_URL=http://192.168.178.11:7333
       depends_on:
         iptvnator-backend:
           condition: service_healthy
       healthcheck:
         test: ["CMD-SHELL", "wget -q --spider http://127.0.0.1 || exit 1"]
         interval: 30s
         timeout: 10s
         retries: 5
         start_period: 20s
       networks:
         - iptv-net

   networks:
     iptv-net:
       driver: bridge
