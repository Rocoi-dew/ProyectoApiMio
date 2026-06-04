# AprenTIC Campus API

API REST para la gestión académica de un bootcamp multi-campus, construida con **Node.js**, **Express** y **MongoDB Atlas**.

---

## Índice

1. [Modelo lógico para MongoDB](#modelo-lógico-para-mongodb)
2. [Arquitectura MVC](#arquitectura-mvc)
3. [CRUD implementado](#crud-implementado)

---

## Modelo lógico para MongoDB

Este proyecto implementa una base de datos **no relacional** con **MongoDB Atlas**. El modelo lógico no se traduce a tablas SQL, sino a colecciones de documentos. Las relaciones entre entidades se representan mediante **referencias con `ObjectId`**, especialmente en las colecciones `alumnos`, `cursos`, `proyectos` y `notas`.

### Colecciones principales

| Colección | Descripción |
|-----------|-------------|
| `Admin` | Usuario con acceso total al sistema |
| `Alumno` | Estudiante perteneciente a un curso |
| `Profesor` | Docente que imparte cursos y corrige notas |
| `Curso` | Agrupación de alumnos por campus y promoción |
| `Proyecto` | Entregable evaluable dentro de un curso |
| `Nota` | Relación entre alumno, proyecto y profesor |

### Relaciones

```
Curso
└── tiene muchos Alumnos
└── tiene muchos Proyectos

Profesor
└── imparte muchos Cursos
└── corrige muchas Notas

Alumno
└── pertenece a un Curso
└── tiene muchas Notas

Proyecto
└── tiene muchas Notas

Nota
└── conecta Alumno + Proyecto + Profesor
```

### Esquema de colecciones

```
ADMIN
├── _id
├── nombre
├── email
├── password
└── rol

PROFESOR
├── _id
├── nombre
├── apellidos
├── email
├── especialidad
└── cursos: [cursoId]

ALUMNO
├── _id
├── nombre
├── apellidos
├── email
├── edad
├── campus
└── cursoId

CURSO
├── _id
├── nombre
├── promocion
├── campus
├── fechaInicio
├── fechaFin
└── profesorId

PROYECTO
├── _id
├── nombre
├── descripcion
├── cursoId
└── fechaEntrega

NOTA
├── _id
├── alumnoId
├── proyectoId
├── profesorId
├── cursoId
├── calificacion
├── estado
└── observaciones
```

---

## Arquitectura MVC

El proyecto sigue el patrón **Model–View–Controller** con las responsabilidades bien separadas en cada capa:

| Capa | Responsabilidad |
|------|----------------|
| `routes/` | Mapean las URLs a los controladores correspondientes |
| `controllers/` | Reciben la petición HTTP y devuelven la respuesta |
| `services/` | Contienen la lógica de negocio y las consultas a la base de datos |
| `models/` | Definen los esquemas de Mongoose para cada colección |

### Estructura de carpetas

```
src/
├── app.js
├── routes/
│   ├── alumnoRoutes.js
│   ├── profesorRoutes.js
│   ├── adminRoutes.js
│   ├── proyectoRoutes.js
│   ├── notaRoutes.js
│   └── cursoRoutes.js
├── controllers/
│   ├── alumnoController.js
│   ├── profesorController.js
│   ├── adminController.js
│   ├── proyectoController.js
│   ├── notaController.js
│   └── cursoController.js
├── services/
│   ├── alumnoService.js
│   ├── profesorService.js
│   ├── adminService.js
│   ├── proyectoService.js
│   ├── notaService.js
│   └── cursoService.js
└── models/
    ├── Alumno.js
    ├── Profesor.js
    ├── Admin.js
    ├── Proyecto.js
    ├── Nota.js
    └── Curso.js
```

---

## CRUD implementado

CRUD completo sobre 6 recursos: **Alumnos**, **Profesores**, **Admins**, **Proyectos**, **Notas** y **Cursos**.

### Alumnos

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| `GET` | `/alumnos` | Obtener todos los alumnos |
| `GET` | `/alumnos/:id` | Obtener un alumno por ID |
| `POST` | `/alumnos` | Crear un nuevo alumno |
| `PUT` | `/alumnos/:id` | Actualizar un alumno |
| `DELETE` | `/alumnos/:id` | Eliminar un alumno |

### Profesores

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| `GET` | `/profesores` | Obtener todos los profesores |
| `GET` | `/profesores/:id` | Obtener un profesor por ID |
| `POST` | `/profesores` | Crear un nuevo profesor |
| `PUT` | `/profesores/:id` | Actualizar un profesor |
| `DELETE` | `/profesores/:id` | Eliminar un profesor |

### Admins

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| `GET` | `/admins` | Obtener todos los admins |
| `GET` | `/admins/:id` | Obtener un admin por ID |
| `POST` | `/admins` | Crear un nuevo admin |
| `PUT` | `/admins/:id` | Actualizar un admin |
| `DELETE` | `/admins/:id` | Eliminar un admin |

### Proyectos

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| `GET` | `/proyectos` | Obtener todos los proyectos |
| `GET` | `/proyectos/:id` | Obtener un proyecto por ID |
| `POST` | `/proyectos` | Crear un nuevo proyecto |
| `PUT` | `/proyectos/:id` | Actualizar un proyecto |
| `DELETE` | `/proyectos/:id` | Eliminar un proyecto |

### Notas

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| `GET` | `/notas` | Obtener todas las notas |
| `GET` | `/notas/:id` | Obtener una nota por ID |
| `POST` | `/notas` | Crear una nueva nota |
| `PUT` | `/notas/:id` | Actualizar una nota |
| `DELETE` | `/notas/:id` | Eliminar una nota |

### Cursos

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| `GET` | `/cursos` | Obtener todos los cursos |
| `GET` | `/cursos/:id` | Obtener un curso por ID |
| `POST` | `/cursos` | Crear un nuevo curso |
| `PUT` | `/cursos/:id` | Actualizar un curso |
| `DELETE` | `/cursos/:id` | Eliminar un curso |

---

## Instalación y ejecución

```bash
# Instalar dependencias
npm install

# Arrancar en modo desarrollo
npm run dev
```

---

*Proyecto realizado para el módulo AprenTIC Full Stack Web — Sevilla*
