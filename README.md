# Levantar PostgreSQL con Docker y Drizzle ORM

Proyecto académico para practicar la configuración de una base de datos **PostgreSQL** mediante **Docker Compose**, junto con la definición de tablas y la gestión de migraciones usando **TypeScript** y **Drizzle ORM**.

**Autor:** Marlon Aguilar  
**GitHub:** [Mar-AV](https://github.com/Mar-AV)

## Objetivos

- Levantar PostgreSQL 16 mediante Docker.
- Conectar el proyecto a la base de datos con una variable de entorno.
- Definir una tabla de usuarios con Drizzle ORM.
- Crear y aplicar migraciones con Drizzle Kit.
- Conservar los datos usando un volumen de Docker.

## Tecnologías utilizadas

- **PostgreSQL 16:** base de datos relacional.
- **Docker y Docker Compose:** contenedores.
- **Node.js y TypeScript:** entorno y lenguaje de desarrollo.
- **Drizzle ORM y Drizzle Kit:** esquema y migraciones.
- **pg y dotenv:** conexión y variables de entorno.

## Requisitos previos

- [Node.js](https://nodejs.org/) y npm.
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) abierto y funcionando.
- Git, para clonar el repositorio.

## Instalación

### 1. Clonar el proyecto

```bash
git clone https://github.com/Mar-AV/Tarea_Levantar_Postgresql_MarlonAguilar.git
cd Tarea_Levantar_Postgresql_MarlonAguilar
```

### 2. Instalar dependencias

```bash
npm install
```

### 3. Levantar PostgreSQL

```bash
docker compose up -d
```

Comprobar el estado del contenedor:

```bash
docker compose ps
```

El archivo `docker-compose.yml` utiliza PostgreSQL 16, el puerto **5432** y un volumen llamado `postgres_data` para conservar los datos.

### 4. Configurar la conexión

Crear un archivo `.env` en la raíz del proyecto y configurar la URL según los datos definidos en `docker-compose.yml`:

```env
DATABASE_URL=postgresql://USUARIO:CONTRASENA@localhost:5432/NOMBRE_BASE_DE_DATOS
```

Reemplazar los valores de ejemplo por los de tu entorno local. **Nunca publicar contraseñas ni archivos `.env` en GitHub.**

### 5. Aplicar las migraciones

Con Docker y PostgreSQL activos y la variable `DATABASE_URL` configurada:

```bash
npx drizzle-kit migrate
```

Si modificas el esquema, genera una nueva migración y aplícala:

```bash
npx drizzle-kit generate
npx drizzle-kit migrate
```

## Estructura del proyecto

```text
Tarea_Levantar_Postgresql_MarlonAguilar/
├── src/
│   └── db/
│       └── schema.ts          # Definición de tablas
├── drizzle/                   # Migraciones
├── docker-compose.yml         # Contenedor PostgreSQL
├── drizzle.config.ts          # Configuración de Drizzle Kit
├── package.json               # Dependencias
└── .env                       # Configuración local, no publicar
```

## Tabla de usuarios

En `src/db/schema.ts` se define la tabla `users`:

| Campo | Tipo | Descripción |
| --- | --- | --- |
| `id` | Entero | Identificador único autogenerado y clave primaria. |
| `name` | VARCHAR(255) | Nombre obligatorio. |
| `age` | Entero | Edad obligatoria. |
| `email` | VARCHAR(255) | Correo obligatorio y único. |

## Comandos útiles

```bash
docker compose ps       # Ver el estado de los contenedores
docker compose logs     # Consultar registros
docker compose down     # Detener y retirar contenedores
```

> **Nota:** No ejecutar `docker compose down -v` si deseas conservar los datos, porque también elimina el volumen de la base de datos.

## Seguridad y buenas prácticas

- Agregar `.env` y `node_modules/` a `.gitignore`.
- Usar credenciales locales de prueba y cambiar las que se hayan publicado.
- No guardar contraseñas reales directamente en los archivos del repositorio.
- Mantener los archivos de migración bajo control de versiones.

## Conclusión

Esta práctica permite comprender cómo levantar un servidor PostgreSQL con Docker, configurar una conexión desde un proyecto Node.js y definir un modelo básico de usuarios utilizando Drizzle ORM. Es una base útil para futuros proyectos que necesiten almacenar información de forma estructurada.
