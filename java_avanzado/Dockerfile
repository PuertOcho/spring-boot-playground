# Usamos Ubuntu 22.04 como base
FROM ubuntu:22.04

# Instalamos dependencias básicas
RUN apt-get update && apt-get install -y \
    openjdk-21-jdk \
    maven \
    curl \
    git \
    wget \
    lsb-release \
    ca-certificates \
    software-properties-common \
    apt-transport-https \
    gnupg2 \
    && apt-get clean

# Instalar Visual Studio Code
RUN curl -sSL https://packages.microsoft.com/keys/microsoft.asc | tee /etc/apt/trusted.gpg.d/microsoft.asc
RUN echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" | tee /etc/apt/sources.list.d/vscode.list
RUN apt-get update && apt-get install -y code

# Establecemos el directorio de trabajo
WORKDIR /app

# Copiamos el archivo pom.xml y el código fuente desde el subdirectorio "demo"
COPY demo/pom.xml .
COPY demo/src ./src

# Copiamos el Maven Wrapper y el directorio .mvn (asegúrate de que esté presente)
COPY demo/mvnw .
COPY demo/mvnw.cmd .
COPY demo/.mvn ./.mvn

# Otorgamos permisos de ejecución al script mvnw
RUN chmod +x mvnw

# Ejecutamos Maven para descargar las dependencias y construir el proyecto
RUN ./mvnw clean install

# Exponemos el puerto 8080 (ajusta este puerto si tu app usa otro)
EXPOSE 8080

# Comando por defecto para ejecutar la aplicación Spring Boot
CMD ["./mvnw", "spring-boot:run"]

