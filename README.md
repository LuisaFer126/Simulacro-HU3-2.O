🌐 Simulacro-HU3 – API REST de Usuarios y Productos (JWT + Docker + MySQL)

📘 Descripción General

Simulacro-HU3 es una API REST desarrollada en ASP.NET Core (.NET 8) con arquitectura por capas y autenticación basada en JSON Web Tokens (JWT).
El sistema permite la gestión de usuarios y productos, integrando operaciones CRUD protegidas con roles y tokens de acceso.

Este proyecto fue creado con fines académicos, siguiendo buenas prácticas de arquitectura limpia, seguridad, pruebas unitarias y despliegue con Docker.

🎯 Objetivos del Sistema

Registro e inicio de sesión con JWT.
Gestión de usuarios (roles: Admin y User).
CRUD completo de productos.
Protección de endpoints mediante autorización.
Base de datos en MySQL, con soporte para migraciones EF Core.
Despliegue vía Docker (API + DB).
Documentación con Swagger.

2 pruebas unitarias en la capa Application.

🏗️ Arquitectura del Proyecto

El proyecto sigue el estilo de Clean Architecture, separando responsabilidades en 4 capas:

Simulacro-HU3/
│
├── Simulacro-HU3.Api/             → Capa de presentación (Controllers, configuración JWT, Swagger)
├── Simulacro-HU3.Application/     → Lógica de negocio (Servicios, Validaciones, DTOs)
├── Simulacro-HU3.Domain/          → Entidades e Interfaces
├── Simulacro-HU3.Infraestructure/ → Acceso a datos, EF Core, Repositorios, Migraciones
└── compose.yml / Dockerfile       → Contenedores (API + MySQL)


✅ Bajo acoplamiento
✅ Alta cohesión
✅ Escalabilidad y mantenibilidad

🛠️ Tecnologías Utilizadas

.NET 8 – ASP.NET Core

Entity Framework Core – MySQL

JWT (JSON Web Tokens)

C# 12

Docker & Docker Compose

Swagger / Swashbuckle

MySQL 8

Rider / Visual Studio / VS Code

⚙️ Configuración y Ejecución
✅ Requisitos Previos

.NET SDK 8.0

Docker Desktop

Rider, Visual Studio o VS Code

✅ 1. Clonar el repositorio
git clone https://github.com/LuisaFer126/Simulacro-HU3-2.O.git
cd Simulacro-HU3

✅ 2. Configurar el appsettings.json

Archivo:

Simulacro-HU3.Api/appsettings.json

Ejemplo:

"ConnectionStrings": {
"DefaultConnection": "server=localhost;port=3307;database=SimulacroDb;user=root;password=rootpass;"
},
"Jwt": {
"Key": "ESTA_ES_LA_CLAVE_SUPER_SECRETA"
}

✅ 3. Levantar MySQL con Docker
docker-compose up -d


Esto levanta:
✅ MySQL
✅ Puerto 3307
✅ Red docker interna

✅ 4. Ejecutar migraciones
cd Simulacro-HU3.Infraestructure
dotnet ef database update --startup-project ../Simulacro-HU3.Api

✅ 5. Ejecutar la API
cd ../Simulacro-HU3.Api
dotnet run


Luego abre Swagger:

👉 http://localhost:8080/
http://localhost:5268/swagger

🔐 Autenticación JWT

La API usa JWT Bearer Tokens para autenticar usuarios.
Flujo:

El usuario se registra con POST /api/auth/register

Luego inicia sesión con POST /api/auth/login

El servidor devuelve un token JWT válido

El cliente lo envía en los headers:

Authorization: Bearer {token}


✅ Todas las rutas están protegidas excepto Register y Login.

🧾 Endpoints Principales

Controladores ubicados en:
Simulacro-HU3.Api/Controllers/

🔑 AuthController

Ruta base: /api/auth

✅ POST /api/auth/register

Crea un usuario nuevo (Username, Email, Password, Role).
🔓 Público.

✅ POST /api/auth/login

Devuelve:

Token JWT

Datos del usuario autenticado
🔓 Público.

👤 UserController

Ruta base: /api/users

Método	Endpoint	Autorización	Descripción
GET	/api/users	Admin	Lista todos los usuarios
GET	/api/users/{id}	Autenticado	Obtiene usuario por ID
PUT	/api/users/{id}	Autenticado	Actualiza usuario
DELETE	/api/users/{id}	Admin	Elimina usuario
📦 ProductController

Ruta base: /api/products

Método	Endpoint	Autorización	Descripción
POST	/api/products	Autenticado	Crear producto
GET	/api/products	Autenticado	Listar productos
GET	/api/products/{id}	Autenticado	Ver producto
PUT	/api/products/{id}	Autenticado	Actualizar producto
DELETE	/api/products/{id}	Admin	Eliminar producto
🔧 Roles definidos

Archivo:
Simulacro-HU3.Domain/Entities/UserRole.cs

public enum UserRole
{
Admin,
User
}

📦 Docker

El proyecto incluye:

Dockerfile para la API

compose.yml para levantar:
✅ MySQL
✅ API
✅ Red interna

Ejemplo rápido:

docker-compose up -d --build

🧪 Pruebas Unitarias (Application Layer)

Incluye 2 pruebas obligatorias:

✅ Validación de creación de producto
✅ Verificación del login de usuario

📄 Documentación Adicional

Diagramas en:

Incluye:

Diagrama de clases![img.png](img.png)



