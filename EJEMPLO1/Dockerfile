#Indicamos la imagen que vamos a utilizar 
FROM ubuntu:latest

#Instalamos algunas herramientas en linux
RUN apt-get update && apt-get install -y curl wget vim git

#Donde va a ser el espacio de trabajo dentro del contenedor. Aqui se guardaran los archivos necesarios para trabajar con ese container.
WORKDIR /app

#Creamos un archivo de texto dentro del contenedor con un comando linux. 
RUN echo "¡Hola Docker!" > saludo.txt

#Cuando esta imagen se ejecute va a estar expuesta al port 80 para posibles conexiones.
EXPOSE 80

#Comando predeterminado que solo se va a ejecutar cuando este contenedor se inicie. 
CMD ["echo","Este es un contenedor de ejemplo"]