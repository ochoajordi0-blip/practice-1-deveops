# Práctica 1: DevOps - CI/CD con GitHub Actions y Nginx

Este proyecto contiene una práctica de integración continua (CI) y despliegue continuo (CD) hacia un servidor web con **Nginx**.

---

## 📁 Estructura del Proyecto

```text
practice-1-deveops/
├── .github/
│   └── workflows/
│       └── deploy.yml   # Pipeline CI/CD de GitHub Actions
├── index.html           # Página web estática principal
└── README.md            # Documentación del proyecto
```

---

## 🚀 Pasos para Configurar tu Servidor Web (Nginx)

En tu servidor Linux (Ubuntu/Debian), ejecuta los siguientes comandos:

### 1. Actualizar repositorios e instalar Nginx
```bash
sudo apt update
sudo apt install -y nginx
```

### 2. Verificar que Nginx esté corriendo
```bash
sudo systemctl status nginx
sudo systemctl enable nginx
sudo systemctl start nginx
```

### 3. Ajustar permisos en la carpeta web
Permite que el usuario SSH pueda escribir en `/var/www/html`:
```bash
sudo chown -R $USER:$USER /var/www/html
sudo chmod -R 755 /var/www/html
```

---

## 🔐 Configuración de Secretos en GitHub

En tu repositorio de GitHub, ve a **Settings** > **Secrets and variables** > **Actions** > **New repository secret** y agrega:

| Nombre del Secreto | Descripción | Ejemplo |
| :--- | :--- | :--- |
| `SERVER_HOST` | Dirección IP o dominio de tu servidor | `192.168.1.100` o `mi-servidor.com` |
| `SERVER_USER` | Usuario con acceso SSH en el servidor | `ubuntu` o `root` |
| `SSH_PRIVATE_KEY` | Clave privada SSH (`id_rsa` / `id_ed25519`) | `-----BEGIN OPENSSH PRIVATE KEY----- ...` |
| `SERVER_PASSWORD` | *(Opcional)* Si te conectas por contraseña | `tu_password` |
| `SERVER_PORT` | *(Opcional)* Puerto SSH (por defecto 22) | `22` |

---

## 🔄 Flujo CI/CD

1. **CI (Continuous Integration):**
   - Comprueba la existencia y sintaxis básica de `index.html`.
2. **CD (Continuous Deployment):**
   - Copia automáticamente `index.html` a `/var/www/html` en el servidor usando SCP.
   - Recarga el servicio Nginx con `sudo systemctl reload nginx`.
