#TODO: Solicita a docker que obtenga la siguiente imagen. 
#TODO: Docker va a buscar la imagen oficial del sdk de .net 6.0 y se renombra a 'build'
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build

#TODO: Define un nombre para la aplicación (en este caso 'webapp')
#TODO: Este es un nombre para el contenedor
WORKDIR webapp

#TODO: Expone los puertos 80 y 5024 (Este último fue el que se definio en el método 'CreateHostBuilder' de la clase 'Program.cs')
EXPOSE 80
EXPOSE 5024

#TODO: Copia los archivos de proyecto en el mismo directorio
#TODO: Archivos que estén en el directorio en el cual está ubicado (este archivo ''DockerFile'. Por esta razón se creó el DockerFile a nivel del archivo de proyecto 'DockerDotNetApp.csproj')
COPY ./*.csproj ./

#TODO: Verifica que el archivo de proyecto tenga todas las dependencias que necesita.
RUN dotnet restore

#TODO: Copia el resto de las cosas.
#TODO: Copia el resto al mismo contenedor.
#TODO: Estamos moviendo archivos desde el build de esta aplicacion hacia adentro del contenedor de docker
COPY . .

#TODO: Obtiene los artefactos que docker va a necesitar para ejecutar la aplicación (tomar las dll's y ejecutarlas)
RUN dotnet publish -c Release -o out

#TODO: Construir la imagen (hacer un build de la imagen) que luego se va a agregar a un contenedor.
FROM mcr.microsoft.com/dotnet/sdk:6.0
WORKDIR /webapp
COPY --from=build /webapp/out .
ENTRYPOINT ["dotnet", "DockerDotNetApp.dll"]