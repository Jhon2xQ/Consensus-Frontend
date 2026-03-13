# Electoral Process API Documentation

## Base URL

```
/api/electoral-process
```

## Authentication

Todos los endpoints requieren autenticación mediante better-auth.


## Roles

- **ADMIN**: Acceso completo (crear, actualizar, desactivar, leer)
- **VOTER**: Solo lectura (listar y obtener por ID)

---

## Endpoints

### 1. Crear Proceso Electoral

Crea un nuevo proceso electoral.

**Endpoint:** `POST /api/electoral-process`

**Roles permitidos:** `ADMIN`

**Request Body:**

```json
{
  "name": "string (1-255 caracteres, requerido)",
  "description": "string (requerido)",
  "globalSdate": "ISO 8601 date (requerido)",
  "globalEdate": "ISO 8601 date (requerido)",
  "commitmentSdate": "ISO 8601 date (requerido)",
  "commitmentEdate": "ISO 8601 date (requerido)",
  "votingSdate": "ISO 8601 date (requerido)",
  "votingEdate": "ISO 8601 date (requerido)",
  "resultsDate": "ISO 8601 date (requerido)"
}
```

**Validaciones de fechas:**

- `globalSdate` < `globalEdate`
- `commitmentSdate` >= `globalSdate`
- `commitmentEdate` <= `globalEdate`
- `commitmentSdate` < `commitmentEdate`
- `votingSdate` >= `commitmentEdate`
- `votingEdate` <= `globalEdate`
- `votingSdate` < `votingEdate`
- `resultsDate` >= `votingEdate`
- `resultsDate` <= `globalEdate`

**Ejemplo de Request:**

```json
{
  "name": "Elecciones Estudiantiles 2026",
  "description": "Proceso electoral para elegir representantes estudiantiles del período 2026-2027",
  "globalSdate": "2026-04-01T00:00:00Z",
  "globalEdate": "2026-05-31T23:59:59Z",
  "commitmentSdate": "2026-04-01T00:00:00Z",
  "commitmentEdate": "2026-04-15T23:59:59Z",
  "votingSdate": "2026-05-01T00:00:00Z",
  "votingEdate": "2026-05-15T23:59:59Z",
  "resultsDate": "2026-05-20T00:00:00Z"
}
```

**Response:** `201 Created`

```json
{
  "success": true,
  "message": "Proceso electoral creado exitosamente",
  "data": {
    "id": "uuid",
    "name": "Elecciones Estudiantiles 2026",
    "description": "Proceso electoral para elegir representantes estudiantiles del período 2026-2027",
    "globalSdate": "2026-04-01T00:00:00.000Z",
    "globalEdate": "2026-05-31T23:59:59.000Z",
    "commitmentSdate": "2026-04-01T00:00:00.000Z",
    "commitmentEdate": "2026-04-15T23:59:59.000Z",
    "votingSdate": "2026-05-01T00:00:00.000Z",
    "votingEdate": "2026-05-15T23:59:59.000Z",
    "resultsDate": "2026-05-20T00:00:00.000Z",
    "isActive": true,
    "creatorId": "uuid",
    "createdAt": "2026-03-13T14:30:00.000Z",
    "updatedAt": "2026-03-13T14:30:00.000Z"
  }
}
```

---

### 2. Listar Procesos Electorales

Obtiene una lista de procesos electorales con filtros opcionales.

**Endpoint:** `GET /api/electoral-process`

**Roles permitidos:** `ADMIN`, `VOTER`

**Query Parameters:**

| Parámetro   | Tipo    | Requerido | Descripción                                    |
| ----------- | ------- | --------- | ---------------------------------------------- |
| `isActive`  | boolean | No        | Filtra por estado activo/inactivo              |
| `creatorId` | string  | No        | Filtra por ID del usuario que creó el proceso  |

**Ejemplos de Request:**

```bash
# Obtener todos los procesos
GET /api/electoral-process

# Obtener solo procesos activos
GET /api/electoral-process?isActive=true

# Obtener procesos de un creador específico
GET /api/electoral-process?creatorId=uuid-del-creador

# Combinar filtros
GET /api/electoral-process?isActive=true&creatorId=uuid-del-creador
```

**Response:** `200 OK`

```json
{
  "success": true,
  "message": "Procesos electorales obtenidos exitosamente",
  "data": [
    {
      "id": "uuid",
      "name": "Elecciones Estudiantiles 2026",
      "description": "Proceso electoral para elegir representantes estudiantiles del período 2026-2027",
      "globalSdate": "2026-04-01T00:00:00.000Z",
      "globalEdate": "2026-05-31T23:59:59.000Z",
      "commitmentSdate": "2026-04-01T00:00:00.000Z",
      "commitmentEdate": "2026-04-15T23:59:59.000Z",
      "votingSdate": "2026-05-01T00:00:00.000Z",
      "votingEdate": "2026-05-15T23:59:59.000Z",
      "resultsDate": "2026-05-20T00:00:00.000Z",
      "isActive": true,
      "creatorId": "uuid",
      "createdAt": "2026-03-13T14:30:00.000Z",
      "updatedAt": "2026-03-13T14:30:00.000Z"
    }
  ]
}
```

---

### 3. Obtener Proceso Electoral por ID

Obtiene los detalles de un proceso electoral específico.

**Endpoint:** `GET /api/electoral-process/:id`

**Roles permitidos:** `ADMIN`, `VOTER`

**Path Parameters:**

| Parámetro | Tipo   | Descripción                      |
| --------- | ------ | -------------------------------- |
| `id`      | string | UUID del proceso electoral       |

**Ejemplo de Request:**

```bash
GET /api/electoral-process/550e8400-e29b-41d4-a716-446655440000
```

**Response:** `200 OK`

```json
{
  "success": true,
  "message": "Proceso electoral obtenido exitosamente",
  "data": {
    "id": "550e8400-e29b-41d4-a716-446655440000",
    "name": "Elecciones Estudiantiles 2026",
    "description": "Proceso electoral para elegir representantes estudiantiles del período 2026-2027",
    "globalSdate": "2026-04-01T00:00:00.000Z",
    "globalEdate": "2026-05-31T23:59:59.000Z",
    "commitmentSdate": "2026-04-01T00:00:00.000Z",
    "commitmentEdate": "2026-04-15T23:59:59.000Z",
    "votingSdate": "2026-05-01T00:00:00.000Z",
    "votingEdate": "2026-05-15T23:59:59.000Z",
    "resultsDate": "2026-05-20T00:00:00.000Z",
    "isActive": true,
    "creatorId": "uuid",
    "createdAt": "2026-03-13T14:30:00.000Z",
    "updatedAt": "2026-03-13T14:30:00.000Z"
  }
}
```

**Error Response:** `404 Not Found`

```json
{
  "success": false,
  "message": "Proceso electoral no encontrado con ID: 550e8400-e29b-41d4-a716-446655440000"
}
```

---

### 4. Actualizar Proceso Electoral

Actualiza un proceso electoral existente.

**Endpoint:** `PUT /api/electoral-process/:id`

**Roles permitidos:** `ADMIN`

**Path Parameters:**

| Parámetro | Tipo   | Descripción                      |
| --------- | ------ | -------------------------------- |
| `id`      | string | UUID del proceso electoral       |

**Request Body:**

Todos los campos son opcionales, pero si se actualizan fechas, deben proporcionarse las 7 fechas.

```json
{
  "name": "string (1-255 caracteres, opcional)",
  "description": "string (opcional)",
  "globalSdate": "ISO 8601 date (opcional)",
  "globalEdate": "ISO 8601 date (opcional)",
  "commitmentSdate": "ISO 8601 date (opcional)",
  "commitmentEdate": "ISO 8601 date (opcional)",
  "votingSdate": "ISO 8601 date (opcional)",
  "votingEdate": "ISO 8601 date (opcional)",
  "resultsDate": "ISO 8601 date (opcional)"
}
```

**Reglas de actualización:**

- Se pueden actualizar `name` y `description` de forma independiente
- Si se actualiza alguna fecha, deben proporcionarse las 7 fechas
- Las fechas deben cumplir las mismas validaciones que en la creación

**Ejemplo de Request (solo nombre y descripción):**

```json
{
  "name": "Elecciones Estudiantiles 2026 - Actualizado",
  "description": "Descripción actualizada del proceso electoral"
}
```

**Ejemplo de Request (actualización completa con fechas):**

```json
{
  "name": "Elecciones Estudiantiles 2026 - Actualizado",
  "description": "Descripción actualizada del proceso electoral",
  "globalSdate": "2026-04-05T00:00:00Z",
  "globalEdate": "2026-06-05T23:59:59Z",
  "commitmentSdate": "2026-04-05T00:00:00Z",
  "commitmentEdate": "2026-04-20T23:59:59Z",
  "votingSdate": "2026-05-05T00:00:00Z",
  "votingEdate": "2026-05-20T23:59:59Z",
  "resultsDate": "2026-05-25T00:00:00Z"
}
```

**Response:** `200 OK`

```json
{
  "success": true,
  "message": "Proceso electoral actualizado exitosamente",
  "data": {
    "id": "uuid",
    "name": "Elecciones Estudiantiles 2026 - Actualizado",
    "description": "Descripción actualizada del proceso electoral",
    "globalSdate": "2026-04-05T00:00:00.000Z",
    "globalEdate": "2026-06-05T23:59:59.000Z",
    "commitmentSdate": "2026-04-05T00:00:00.000Z",
    "commitmentEdate": "2026-04-20T23:59:59.000Z",
    "votingSdate": "2026-05-05T00:00:00.000Z",
    "votingEdate": "2026-05-20T23:59:59.000Z",
    "resultsDate": "2026-05-25T00:00:00.000Z",
    "isActive": true,
    "creatorId": "uuid",
    "createdAt": "2026-03-13T14:30:00.000Z",
    "updatedAt": "2026-03-13T15:45:00.000Z"
  }
}
```

**Error Response:** `400 Bad Request`

```json
{
  "success": false,
  "message": "Si se actualizan fechas, deben proporcionarse todas las 7 fechas"
}
```

---

### 5. Desactivar Proceso Electoral

Desactiva un proceso electoral (soft delete). El proceso no se elimina de la base de datos.

**Endpoint:** `PATCH /api/electoral-process/:id/deactivate`

**Roles permitidos:** `ADMIN`

**Path Parameters:**

| Parámetro | Tipo   | Descripción                      |
| --------- | ------ | -------------------------------- |
| `id`      | string | UUID del proceso electoral       |

**Ejemplo de Request:**

```bash
PATCH /api/electoral-process/550e8400-e29b-41d4-a716-446655440000/deactivate
```

**Response:** `200 OK`

```json
{
  "success": true,
  "message": "Proceso electoral desactivado exitosamente",
  "data": {
    "id": "550e8400-e29b-41d4-a716-446655440000",
    "name": "Elecciones Estudiantiles 2026",
    "description": "Proceso electoral para elegir representantes estudiantiles del período 2026-2027",
    "globalSdate": "2026-04-01T00:00:00.000Z",
    "globalEdate": "2026-05-31T23:59:59.000Z",
    "commitmentSdate": "2026-04-01T00:00:00.000Z",
    "commitmentEdate": "2026-04-15T23:59:59.000Z",
    "votingSdate": "2026-05-01T00:00:00.000Z",
    "votingEdate": "2026-05-15T23:59:59.000Z",
    "resultsDate": "2026-05-20T00:00:00.000Z",
    "isActive": false,
    "creatorId": "uuid",
    "createdAt": "2026-03-13T14:30:00.000Z",
    "updatedAt": "2026-03-13T16:00:00.000Z"
  }
}
```

**Error Response:** `404 Not Found`

```json
{
  "success": false,
  "message": "Proceso electoral no encontrado con ID: 550e8400-e29b-41d4-a716-446655440000"
}
```

---

## Códigos de Estado HTTP

| Código | Descripción                                                  |
| ------ | ------------------------------------------------------------ |
| 200    | Operación exitosa                                            |
| 201    | Recurso creado exitosamente                                  |
| 400    | Error de validación en los datos enviados                    |
| 401    | No autenticado (token faltante o inválido)                   |
| 403    | No autorizado (rol insuficiente)                             |
| 404    | Recurso no encontrado                                        |
| 500    | Error interno del servidor                                   |

---

## Estructura de Respuesta de Error

Todas las respuestas de error siguen este formato:

```json
{
  "success": false,
  "message": "Descripción del error"
}
```

**Ejemplos de errores comunes:**

```json
// Error de validación
{
  "success": false,
  "message": "La fecha de inicio global debe ser anterior a la fecha de fin global"
}

// Error de autenticación
{
  "success": false,
  "message": "Token de autenticación no proporcionado"
}

// Error de autorización
{
  "success": false,
  "message": "Acceso denegado: se requiere rol ADMIN"
}

// Error de recurso no encontrado
{
  "success": false,
  "message": "Proceso electoral no encontrado con ID: 550e8400-e29b-41d4-a716-446655440000"
}
```

---

## Notas Importantes

1. **Soft Delete**: Los procesos electorales nunca se eliminan físicamente de la base de datos, solo se desactivan mediante el campo `isActive`.

2. **Fechas**: Todas las fechas deben enviarse en formato ISO 8601 y se almacenan en UTC.

3. **Validación de fechas**: Las validaciones de fechas se realizan tanto en el schema de Zod como en el caso de uso para garantizar la integridad de los datos.

4. **Autenticación**: Todos los endpoints requieren un token Bearer válido en el header `Authorization`.

5. **Roles**: Los endpoints de escritura (POST, PUT, PATCH) requieren rol `ADMIN`, mientras que los de lectura (GET) están disponibles para `ADMIN` y `VOTER`.
