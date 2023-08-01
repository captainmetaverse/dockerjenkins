# dockerjenkins

### Dockerfile para instalar Docker en el contenedor de Jenkins

## Pasos a seguir:

clona el repositorio y ejecuta desde su raiz 

git clone 

despues crea fuera del directorio ....
el archivo docker-compose.yml
con el siguiente contenido
```
version: '3'
services:
  jenkins:
    image: jenkins/docker
    build:
      context: dockerjenkins
    ports:
      - 8080:8080
      - 50000:50000
    container_name: jenkins
    volumes:
      - $PWD/jenkins_home:/var/jenkins_home
      - /var/run/docker.sock:/var/run/docker.sock
    networks:
      - net
networks:
  net:
```
### Construye las imagenes de los servicios definidos en docker-compose.yml
docker-compose build

### Creacion del contenedor, configuración de redes y volúmenes e inicio de servicios
docker-compose up -d

### Acceder al contenedor siendo root
docker exec -it --user root jenkins bash

### cambia el propietario (owner) del archivo docker.sock al usuario "jenkins"
chown jenkins /var/run/docker.sock

