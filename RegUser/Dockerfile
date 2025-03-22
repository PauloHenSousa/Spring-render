#Etapa de construção
FROM maven:3.4.3-openjdk-21 AS build
#FROM ubuntu:latest AS build

#Definir o diretório dentro do container para a aplicação
WORKDIR /app

#Copiar o pom.xml par o container 
COPY pom.xml .
COPY src ./src

#Executar o maven para compilar o projeto e gerar o arquivo JAR
RUN mvn clean package -DskipTests

#Etapa de execução
FROM openjdk:21-slim

#Definir o diretório de trabalho para a aplicação
WORKDIR /app

#Copiar o JAR construido na etapa anterior
COPY --from=build /app/target/*.JAR app.JAR

#Definir a porta que será utilizada na aplicação
EXPOSE 8189

#Comando para executar a aplicação
ENTRYPOINT ["java", "-jar", app.jar]