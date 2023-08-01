# dockerjenkins

### Dockerfile para instalar Docker en el contenedor de Jenkins

## Pasos a seguir:

1. En Ubuntu crea un directorio jenkins dentro de el directorio /home/<usuario>
2. Dentro del directorio jenkins crea el directorio jenkins_home
3. Clona el repositorio dentro del directorio jenkins 

   git clone https://github.com/captainmetaverse/dockerjenkins.git

5. Crea también dentro del directorio jenkins el archivo docker-compose.yml con el siguiente contenido
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

5. Ejecuta el siguiente comando para contruir las imagenes de los servicios definidos en docker-compose.yml

docker-compose build

6. Ejecuta el siguiente comando para la creación del contenedor, configuración de redes y volúmenes e inicio de servicios

docker-compose up -d

7. Acceder al contenedor siendo root

docker exec -it --user root jenkins bash

8. Cambiar el propietario (owner) del archivo docker.sock al usuario "jenkins"

chown jenkins /var/run/docker.sock

Ahora dentro del contenedor se pueden ejecutar comandos de docker, por ejmplo:  docker ps


