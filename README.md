
<div align="center">
  <h1 align="center">
    Challenge: API REST Foro Hub
    <br />
    <br />

![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=java&logoColor=white) ![Spring](https://img.shields.io/badge/spring-%236DB33F.svg?style=for-the-badge&logo=spring&logoColor=white) ![MySQL](https://img.shields.io/badge/mysql-4479A1.svg?style=for-the-badge&logo=mysql&logoColor=white) ![IntelliJ IDEA](https://img.shields.io/badge/IntelliJIDEA-000000.svg?style=for-the-badge&logo=intellij-idea&logoColor=white)

</h1>
</div>

Este proyecto está diseñado para proporcionarte una plataforma donde puedas aplicar tus conocimientos en Java y SpringBoot para construir un sistema de foro interactivo.

## Descripción

El objetivo de este proyecto de API REST es permitir a los usuarios gestionar tópicos en un foro. Los usuarios podrán realizar las siguientes acciones solo si son autenticados mediante tokens JWT:

✔️ Listar todos los tópicos disponibles.

✔️ Listar tópico por Id, este ingresado en la url.

✔️ Crear nuevos tópicos.

✔️ Modificar topico.

✔️ Eliminar tópicos existentes.

También se dejaron algunas funcionalidades libres para facilitar el desarrollo de pruebas, estas fueron:

✔️ Login de usuario.

✔️ Registrar usuario.

✔️ Registrar curso.


## Tecnologías Utilizadas

**Java:** Lenguaje principal de desarrollo.

**SpringBoot:** Framework para el desarrollo de aplicaciones Java basadas en Spring. 

**JWT (JSON Web Tokens):** Utilizado para la autenticación de usuarios.

**MySQL:** Base de datos para almacenar la información de los tópicos, usuarios y cursos.

**Insomnia:** Herramienta utilizada para probar y documentar los endpoints de la API.

##  Endpoints Disponibles

### GET /topicos

Devuelve una lista de todos los tópicos existentes en el foro. Se requiere autenticación JWT para realizar esta acción.

### GET /topicos/{id}

Devuelve el tópico especificado por su ID. Se requiere autenticación JWT para realizar esta acción.

### POST /topicos

Crea un nuevo tópico en el foro. Se requiere autenticación JWT para realizar esta acción.

Ejemplo de cuerpo de solicitud:

```json
{
	"titulo":"fechas de entrega",
	"mensaje":"Me podrian indicar como quedo el cronograma este semestre",
	"cursoId":"1",
	"autorId":"1"
}
```
### PUT /topicos/{id}

Actualiza el topico especificado en el ID, solo puedes actualizar Titulo y Mensaje. Se requiere autenticación JWT para realizar esta acción.

```json
{
      "titulo":"problema al cargar trabajo",
      "mensaje":"Al cargar el trabajo se genera error"
}
```

### DELETE /topicos/{id}

Elimina el tópico especificado por su ID. Se requiere autenticación JWT para realizar esta acción.

## Autenticación JWT

Para realizar operaciones que modifican el estado del foro (como crear o eliminar tópicos), se requiere autenticación mediante JWT. A continuación se describe el proceso:

1. **Registrar Usuario**:
    - Realiza una solicitud POST a `/usuario` con el cuerpo de la solicitud que incluye nombre, correo y contraseña. Se bebe tener cuidado porque en contraseña debes poner la [**contraseña Bcrypt**](https://www.browserling.com/tools/bcrypt).


   Ejemplo de solicitud:

```json
{
  "nombre":"Samanta Gomez ",
  "correo":"samanta4@gmail.com",
  "contrasena":"$2a$10$.4.p/zSHVFZT8kqlF3egUurTsJ1tkYcBX4WQorVIoUhmpNS59M99G"
}
```

   En este ejemplo se tenia la Password: 1212 entonces su Bcrypt es: $2a$10$.4.p/zSHVFZT8kqlF3egUurTsJ1tkYcBX4WQorVIoUhmpNS59M99G

2. **Registrar curso**:
    - Realiza una solicitud POST a `/curso` con el cuerpo de la solicitud de la siguiente manera:


Ejemplo de solicitud:

```json
{
  "nombre":"CURSO_4"
}
```
3. **Autenticación**:
    - Realiza una solicitud POST a `/login` con el cuerpo de la solicitud que incluye el email y la contraseña del usuario registrado. 

Ejemplo de solicitud:

```json
{
  "correo":"samanta4@gmail.com",
  "contrasena":"1212"
}
```
La respuesta incluirá un token JWT que debe ser incluido en las cabeceras de las solicitudes posteriores como `Authorization: Bearer <token>`.


   