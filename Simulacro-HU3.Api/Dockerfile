# Etapa base: runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

# Etapa build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copiar solución y proyectos
COPY Simulacro-HU3.sln ./
COPY Simulacro-HU3.Api/Simulacro-HU3.Api.csproj Simulacro-HU3.Api/
COPY Simulacro-HU3.Application/Simulacro-HU3.Application.csproj Simulacro-HU3.Application/
COPY Simulacro-HU3.Domain/Simulacro-HU3.Domain.csproj Simulacro-HU3.Domain/
COPY Simulacro-HU3.Infraestructure/Simulacro-HU3.Infraestructure.csproj Simulacro-HU3.Infraestructure/

# Restaurar dependencias
RUN dotnet restore Simulacro-HU3.sln

# Copiar todo el código fuente
COPY . .
# Compilar en modo Release
RUN dotnet build Simulacro-HU3.sln -c Release -o /app/build

# Publicar artefactos
FROM build AS publish
RUN dotnet publish Simulacro-HU3.Api/Simulacro-HU3.Api.csproj -c Release -o /app/publish

# Imagen final
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Simulacro-HU3.Api.dll"]
