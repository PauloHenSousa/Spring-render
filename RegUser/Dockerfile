#Etapa de construção
#FROM maven:3.4.3-openjdk-21 AS build
#FROM ubuntu:latest AS build
FROM openjdk:21-jdk-slim AS build
RUN apt-get update \
    && apt-get install -y maven \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

#Definir o diretório dentro do container para a aplicação
WORKDIR /app

#Copiar o pom.xml para o container 
COPY RegUser/pom.xml .

# Copiar o diretório src para o container
COPY RegUser/src ./src

#Executar o maven para compilar o projeto e gerar o arquivo JAR
RUN mvn clean package -DskipTests

# Verificar o conteúdo do diretório target/ para garantir que o arquivo JAR foi gerado
RUN ls -l /app/target

#Etapa de execução
FROM openjdk:21-slim

#Definir o diretório de trabalho para a aplicação
WORKDIR /app

#Copiar o JAR construido na etapa anterior
COPY --from=build /app/target/*.jar app.jar

#Definir a porta que será utilizada na aplicação
EXPOSE 8189

#Comando para executar a aplicação
ENTRYPOINT ["java", "-jar", "app.jar"]