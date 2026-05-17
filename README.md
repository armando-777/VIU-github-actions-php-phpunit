# VIU ejemplo: Github Actions para PHP con test en PHPUnit
___

## VIU-github-actions-php-phpunit

Proyecto PHP con pruebas unitarias usando PHPUnit, integración continua con
GitHub Actions y despliegue automático de imagen Docker a Docker Hub.

---

## Requisitos previos

- [Git](https://git-scm.com/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [WSL2]
- Cuenta en [Docker Hub](https://hub.docker.com/)

---

## 1. Instalar Docker Desktop

1. Ve a [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
2. Descarga la versión para **Windows**
3. Ejecuta el instalador y sigue los pasos
4. Reinicia el equipo cuando lo solicite
5. Abre Docker Desktop y espera a que el ícono de la ballena aparezca en verde

> **Nota:** Asegúrate de tener WSL2 habilitado. Docker Desktop lo usa como backend en Windows.

---

## 2. Clonar el repositorio

```bash
git clone https://github.com/VicenteMonfort/VIU-github-actions-php-phpunit.git
cd VIU-github-actions-php-phpunit
```

---

## 3. Configurar secretos en GitHub

El workflow de CI/CD necesita acceder a Docker Hub. Ve a:

**Settings → Secrets and variables → Actions → New repository secret**

Agrega los siguientes secretos:

| Nombre | Valor |
|--------|-------|
| `DOCKER_USER` | Tu usuario de Docker Hub |
| `DOCKER_PASSWORD` | Tu token de acceso de Docker Hub |

Para crear el token de Docker Hub:
1. Ve a [https://hub.docker.com](https://hub.docker.com)
2. **Account Settings → Personal access tokens → Generate new token**
3. Copia el token y úsalo como `DOCKER_PASSWORD`

---

## 4. Subir el proyecto a tu propio GitHub

### 4.1 Crear el repositorio en GitHub

1. Ve a [https://github.com](https://github.com)
2. Haz clic en **New repository**
3. Dale el nombre `VIU-github-actions-php-phpunit` y créalo **vacío**

### 5.2 Subir el código

```bash
rm -rf .git
git init
git add .
git commit -m "primer commit"
git remote add origin git@github.com:TU_USUARIO/VIU-github-actions-php-phpunit.git
git branch -M main
git push -u origin main
```
---

## 5. Cómo funciona el CI/CD

El archivo `.github/workflows/cicd-php.yml` define dos jobs:

**CI** — Se ejecuta en cada push:
- Valida `composer.json`
- Instala dependencias
- Ejecuta los tests con PHPUnit

**CD** — Se ejecuta si CI pasa:
- Login a Docker Hub
- Construye la imagen Docker
- Publica la imagen en Docker Hub como `DOCKER_USER/viuejemplo:latest`

![alt text](<Captura de pantalla 2026-05-17 185520.png>)