---
name: 4geeks-academico-proyectos
description: "Cuando se pidan los proyectos académicos asignados, consulta tareas tipo PROJECT y presenta el estado y los datos relevantes de cada una."
---

# Consultar proyectos asignados

## Ejecución

1. Usa `TOKEN_4GEEKS` del entorno; si falta, detente sin leer ni revelar `.env` y explica que OpenClaw no heredó la variable.
2. Usa la API `https://breathecode.herokuapp.com` y la cabecera `Authorization: Token <valor>`. Recupera el usuario actual (`GET /v1/admissions/user/me`) y sus cohortes (`GET /v1/admissions/academy/cohort/me`) para identificar las cohortes activas. No incluyas la credencial en logs o salida.
3. Consulta `GET /v1/assignment/user/me/task` filtrando `task_type=PROJECT`; limita cada consulta a las cohortes del usuario y pagina mediante `limit` y `offset` hasta completar la lista. Si la instancia no acepta un filtro esperado, no sustituyas por una consulta amplia sin delimitarla al usuario.
4. Presenta nombre/título, cohorte si se conoce, fecha límite si existe y estado reportado. Mapea `PENDING` a pendiente, `DONE` a entregado/completado por el estudiante, `APPROVED` a calificado/aprobado, y `REJECTED` a devuelto para correcciones. No infieras una calificación numérica si la respuesta no la incluye.
5. Si falla la API, informa el estado HTTP/categoría del fallo sin incluir credenciales ni datos ajenos al usuario.

## Límites

Solo lectura. No modifiques, entregues ni apruebes proyectos. La referencia describe la forma general de las respuestas; comprueba el esquema real antes de asumir nombres concretos de campos.
