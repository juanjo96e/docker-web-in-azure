# Despliegue de una Web Simple con Docker en Linux y Azure

Este repositorio contiene los pasos esenciales para desplegar una página web básica utilizando Docker en un entorno Linux y, posteriormente, en Azure. La explicación detallada se encuentra en el documento PDF original.

## Requisitos Previos
* Docker instalado en tu sistema Linux (en este caso, WSL).
* Acceso a terminal con privilegios de `sudo`.
* Archivos de la página web (HTML, CSS, etc.) o imagen de Docker preconfigurada.
* Conexión a Internet (opcional si necesitas descargar la imagen).

## Despliegue Local con Docker

1.  **Verificar Docker**: Comprueba la instalación (`docker --version`) o instala si es necesario con `sudo apt update`, `sudo apt install docker.io -y`, `sudo systemctl start docker`, `sudo systemctl enable docker`.
2.  **Crear Directorio**: Navega a tu carpeta de trabajo.
3.  **Crear Archivos Web**: Crea tu `index.html`.
4.  **Crear Dockerfile**: Define la imagen Nginx y copia tu HTML.
5.  **Construir Imagen**: Ejecuta `docker build -t mi-web-docker .`. Puedes usar `sudo docker build -t docker-intro .`.
6.  **Ejecutar Contenedor**: Inicia el contenedor con `docker run -d -p 8080:80 mi-web-docker`. Si usaste `docker-intro`, el comando sería `sudo docker run -d -p 8080:80 docker-intro`.
7.  **Verificar**: Accede a `http://localhost:8080` en tu navegador para comprobar que funciona correctamente en local.
8.  **Opcional: Detener/Eliminar**: Usa `docker stop webdocker` y `docker rm webdocker`.

## Despliegue en Azure

1.  **Instalar Azure CLI**: Ejecuta `curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash`. Verifica con `az version`.
2.  **Iniciar Sesión en Azure**: Usa `az login` y autentícate en el navegador.
3.  **Seleccionar Suscripción**: Elige tu suscripción de Azure.
4.  **Crear Grupo de Recursos**: Crea un grupo con `az group create --name DockerIntroRG --location "westeurope"`.
5.  **Iniciar Sesión en Docker Hub**: Autentícate con `docker login`.
6.  **Etiquetar Imagen**: Etiqueta tu imagen para Docker Hub: `docker tag mi-web-docker tuusuario/mi-web-docker`. Ejemplo: `sudo docker tag docker-intro juanjojkll/docker-intro:v1`.
7.  **Subir Imagen**: Sube la imagen a Docker Hub: `docker push tuusuario/mi-web-docker`.
8.  **Crear Web App en Azure Portal**:
    * Ve a [portal.azure.com](https://portal.azure.com).
    * Busca y selecciona 'Web App'.
    * Haz clic en 'Crear'.
    * Configura en la pestaña 'Básico': Grupo de recursos (`miGrupoDocker`/`DockerIntroRG`), Nombre de la Web App (`miappdocker123` u otro único), Región (misma que el grupo de recursos), `Docker Container` para Publicar, y `Linux` como SO.
9.  **Configurar Contenedor**: En la pestaña `Docker`: Fuente (`Docker Hub`), Tipo (`Imagen de contenedor único`), Nombre de imagen (`tuusuario/mi-web-docker` o `juanjojk11-docker-intro` con la etiqueta), y el puerto `80`.
10. **Revisar y Crear**: Haz clic en 'Review and Create' y luego en 'Crear'.
11. **Acceder a la Web App**: Copia la URL pública desde el recurso Web App (ej. `https://miappdocker123.azurewebsites.net`) y ábrela en tu navegador.

## Ventajas
* **Portabilidad**: Empaqueta la aplicación y sus dependencias, facilitando moverla entre entornos.
* **Escalabilidad**: Permite desplegar múltiples instancias con facilidad.
* **Eficiencia y rapidez**: Contenedores ligeros y de arranque rápido.
* **Consistencia del entorno**: Evita diferencias de configuración entre entornos.
* **Seguridad y aislamiento**: Cada contenedor opera de forma aislada, reduciendo riesgos.

## Autor
**Juanjo Ocón**
Técnico Superior en Administración de Sistemas Informáticos en Red (ASIR)
