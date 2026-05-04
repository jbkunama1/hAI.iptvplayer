# IPTVnator Docker Stack für Portainer

![Docker Image Version](https://img.shields.io/docker/v/4gray/iptvnator/latest?logo=docker&label=iptvnator)
![Docker Image Version](https://img.shields.io/docker/v/4gray/iptvnator-backend/latest?logo=docker&label=backend)
![Build Status](https://github.com/jbkunama1/iptvnator-portainer/actions/workflows/deploy.yml/badge.svg)
![M3U Update](https://github.com/jbkunama1/iptvnator-portainer/actions/workflows/generate_m3u.yml/badge.svg)

Selbstgehosteter IPTV‑Player mit Web‑Frontend und Backend als Docker‑Stack für Portainer.  
Basierend auf [`4gray/iptvnator`](https://github.com/4gray/iptvnator) und [`4gray/iptvnator-backend`](https://github.com/4gray/iptvnator-backend). [web:1][web:2][web:11][web:14]

---

## 📦 Was ist enthalten?

- `docker-compose.yml` für Portainer (Stack‑Import)
- GitHub‑Action, die den Stack automatisch auf Portainer bereitstellt
- GitHub‑Action, die **täglich** eine M3U‑Playlist aus deinem Link aktualisiert
- Badges für Image‑Version, Build‑Status und Schedule

---

## 🚀 Installation auf Docker/Portainer

### Voraussetzungen

- Docker installiert (Standalone oder Swarm)
- Portainer (CE oder BP) [web:7][web:13]

### Schritt 1: Repo in Portainer integrieren

1. In Portainer:  
   **Stacks → Add stack**  
2. Stack‑Name z. B. `iptvnator`  
3. Wähle **Git repository** und trage deine GitHub‑URL ein  
4. Branch z. B. `main`  
5. Git Reference Type: `branch`  
6. Stack‑file: `docker-compose.yml`  
7. **Deploy the stack**

> Alternativ: Lokales `docker-compose.yml` nutzen und in Portainer **Web editor** einfügen.

[web:7][web:13]

---

## 🧩 Portainer + GitHub Actions (CI/CD)

Der Workflow `deploy.yml` verteilt den Stack automatisch auf deinen Portainer‑Host.  
Dazu benötigst du:

- `PORTAINER_URL` (z. B. `https://portainer.example.com`)  
- `PORTAINER_TOKEN` (generiertes API‑Token in Portainer)  
- `DOCKER_REGISTRY` (z. B. `ghcr.io` oder `docker.io`)  
- `DOCKER_IMAGE` (dein Image‑Name, falls du selbst bauen willst, sonst egal)

[web:17][web:19][web:23]

---

## 📺 M3U‑Playlist automatisch täglich hinzufügen

- GitHub‑Action: `generate_m3u.yml`  
- Läuft **täglich** um 03:00 UTC  
- Lädt deine M3U‑URL herunter und legt/speichert sie als `playlist.m3u` im Repo  
- IPTVnator kann dann über einen lokalen Pfad oder URL darauf zugreifen

[web:21][web:27]

---

## 🧰 Anpassungen

- IP/Port: In `docker-compose.yml` `CLIENT_URL` und `BACKEND_URL` + `ports` anpassen  
- M3U‑URL: In `generate_m3u.yml` `INPUT_M3U_URL` ändern  
- Schedule: `on: schedule` in `generate_m3u.yml` anpassen

---

## 📝 Weitere Infos

- Projektseite:  
  https://github.com/4gray/iptvnator [web:14]
- Backend‑Repo:  
  https://github.com/4gray/iptvnator-backend [web:2]
- Docker‑Images:  
  https://hub.docker.com/r/4gray/iptvnator [web:1]  
  https://hub.docker.com/r/4gray/iptvnator-backend [web:3]
