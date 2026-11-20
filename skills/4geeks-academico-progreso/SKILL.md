---
name: 4geeks-academico-progreso
description: "Cuando se solicite un resumen del progreso en el curso, combina cohorte activa, estado de tareas y actividad propia en una síntesis con límites explícitos."
---

# Resumen de progreso académico

## Ejecución

1. Lee `TOKEN_4GEEKS` del entorno. Si falta, detente sin consultar ni mostrar `.env` y comunica que la variable debe estar disponible para el proceso.
2. Usa `https://breathecode.herokuapp.com` con `Authorization: Token <valor>` y consulta usuario y cohortes con `GET /v1/admissions/user/me` y `GET /v1/admissions/academy/cohort/me`. Selecciona la cohorte `ACTIVE`; si hay más de una, informa cuáles se incluyeron.
3. Recupera todas las páginas de `GET /v1/assignment/user/me/task` delimitadas a las cohortes activas. Cuenta por estado (`PENDING`, `DONE`, `APPROVED`, `REJECTED`) y tipo; diferencia completadas por el estudiante de aprobadas por revisión.
4. Consulta `GET /v1/activity/me` para la cohorte activa y, cuando resulte útil, fecha de inicio del curso hasta hoy. Resume solo métricas presentes en la respuesta (por ejemplo, tiempo o ejercicios); no inventes porcentajes de avance.
5. Presenta el intervalo y cohortes usados, recuentos/estados de tareas, métricas de actividad y límites de los datos. Si no hay un total curricular verificable, no expreses el progreso como porcentaje. Señala errores, resultados parciales o ausencia de datos.
6. No reveles el token ni incluyas datos personales de terceros. No registres la cabecera de autorización.

## Límites

Solo lectura. No actualices ni entregues tareas. La actividad es una señal de participación, no necesariamente una medida completa de dominio o finalización del curso; explica esa limitación.
