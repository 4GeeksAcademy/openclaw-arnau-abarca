---
name: 4geeks-academico-pendientes
description: "Cuando se pregunte qué falta completar en 4Geeks, lista tareas pendientes o rechazadas del usuario con detalles que indiquen el siguiente trabajo."
---

# Consultar trabajo pendiente

## Ejecución

1. Lee `TOKEN_4GEEKS` del entorno. Si no está disponible, detente y explica el requisito; no leas ni muestres `.env`.
2. Solicita `GET /v1/admissions/user/me` y `GET /v1/admissions/academy/cohort/me` en `https://breathecode.herokuapp.com` con `Authorization: Token <valor>` para delimitar la consulta a cohortes activas del usuario. Nunca registres ni reveles el token.
3. Recupera `GET /v1/assignment/user/me/task` para dichas cohortes, paginando con `limit` y `offset`. Incluye estados `PENDING` y `REJECTED`; conserva `task_type` y metadatos de fechas.
4. Para elementos rechazados o con descripción insuficiente, usa `GET /v1/assignment/task/{task_id}` para leer instrucciones y feedback. No pidas detalle para tareas ya resueltas si no aporta a la petición.
5. Resume qué tarea falta, por qué (usa descripción/feedback literal resumido), fecha límite si existe y el siguiente paso sugerido. Separa claramente los datos devueltos por la API de cualquier recomendación inferida. Si no hay pendientes, indícalo según los resultados consultados.
6. Si hay error o paginación incompleta, decláralo y no presentes el resultado como una lista completa.

## Límites

Solo lectura: nunca actualices ni entregues una tarea. No inventes requisitos ni fechas. No uses consultas que puedan mostrar datos de otros estudiantes.
