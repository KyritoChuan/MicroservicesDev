FROM mcr.microsoft.com/dotnet/aspnet:5.0-alpine3.16 AS base
WORKDIR /app
EXPOSE 80

# Download Runtime 

FROM mcr.microsoft.com/dotnet/sdk:5.0-alphine3.16 AS build
WORKDIR /src
COPY ./Servicios.api.Libreria.csproj ./
RUN dotnet restore ./Servicios.api.Libreria.csproj
COPY . .
WORKDIR /src/Servicios.api/Libreria
RUN dotnet build ./Servicios.api.Libreria.csproj -c Release -o /app/build

FROM build AS publish
RUN dotnet publish ./Servicios.api.Libreria.csproj -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Servicios.api.Libreria.dll"]
