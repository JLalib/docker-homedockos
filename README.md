# HomeDock OS – Plataforma de gestión Docker autoalojada

**HomeDock OS** es una plataforma *self-hosted* diseñada para simplificar la gestión de servicios Docker mediante una interfaz web moderna, modular y orientada a usuarios que administran múltiples contenedores y stacks en su servidor doméstico o VPS.

Repositorio oficial: https://github.com/BansheeTech/HomeDockOS

---

## ✨ Características principales

- 🐳 Gestión centralizada de contenedores Docker.
- 📦 Organización de aplicaciones mediante stacks.
- 🧩 Sistema de paquetes y extensiones.
- 📂 Exploración y gestión de archivos integrada.
- 🖥 Interfaz web moderna y fácil de usar.
- 🔌 Acceso directo al socket Docker para control total.
- 🏠 Pensado para *homelabs* y entornos autoalojados.

---

## 🐳 Despliegue con Docker Compose

Este repositorio utiliza la imagen oficial de **HomeDock OS** y monta los volúmenes necesarios para persistencia de datos, configuración y gestión de stacks Docker.

### 📄 docker-compose.yml

```yaml
services:

  homedock:
    image: bansheetech/homedock-os:latest
    container_name: homedock-os
    restart: unless-stopped
    ports:
      - "8200:80"
    volumes:
      - ./_DATA/DATA:/DATA
      - ./_DATA/config:/homedock/config
      - ./_DATA/compose:/homedock/compose-link
      - ./_DATA/packages:/homedock/_user_packages
      - ./_DATA/dropzone:/homedock/dropzone
      - ./_DATA/logs:/homedock/logs
      - /var/run/docker.sock:/var/run/docker.sock
    extra_hosts:
      - "host.docker.internal:host-gateway"
    labels:
      - "HDDockerInDocker=true"
    environment:
      - TZ=Europe/Madrid
      - PYTHONUNBUFFERED=1
```

---

## 📁 Estructura de volúmenes

| Ruta local             | Descripción                                  |
|------------------------|----------------------------------------------|
| `_DATA/DATA`           | Datos generales de HomeDock                  |
| `_DATA/config`         | Configuración de la aplicación               |
| `_DATA/compose`        | Enlaces a docker-compose externos            |
| `_DATA/packages`       | Paquetes personalizados del usuario          |
| `_DATA/dropzone`       | Área de carga rápida de archivos             |
| `_DATA/logs`           | Logs de la aplicación                        |
| `/var/run/docker.sock` | Control directo del daemon Docker            |

---

## 🚀 Puesta en marcha

1. Crea la estructura de carpetas:
```bash
mkdir -p _DATA/{DATA,config,compose,packages,dropzone,logs}
```

2. Inicia el contenedor:
```bash
docker compose up -d
```

3. Accede a HomeDock OS desde tu navegador:
```
http://TU_IP:8200
```

---

## 🔐 Seguridad

⚠️ HomeDock OS requiere acceso al socket Docker (`/var/run/docker.sock`), lo que otorga control total sobre el sistema Docker.

**Recomendaciones:**
- No exponer el servicio directamente a Internet.
- Usar VPN o proxy inverso con autenticación.
- Mantener el sistema y las imágenes Docker actualizadas.

---

## 🔄 Actualización

```bash
docker compose pull
docker compose up -d
```

---

## 📘 Recursos

- Repositorio oficial: https://github.com/BansheeTech/HomeDockOS
- Docker Hub: https://hub.docker.com/r/bansheetech/homedock-os

---

## 👤 Autor

README generado para **JLalib** siguiendo el método **README Pro GitHub**.

