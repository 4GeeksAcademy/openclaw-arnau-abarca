# Registro de pruebas de skills académicas 4Geeks

Fecha de la prueba: 2026-11-20 (UTC)

## Prompt original utilizado

> Quiero realizar pruebas para testear cada skill.
> 1. Verifica que la sesion esta activa.
> 2. Generame una lista de los proyectos y su estado.
> 3. Listame el trabajo pendiente
> 4. Dame una descripcion del progreso general del curso y lo que queda.
> Sintetiza esta informacion en una salida

## 1. `4geeks-academico-autenticar`

- **Objetivo:** verificar que el token permite acceder a la sesión académica sin revelar la credencial.
- **Endpoint utilizado:** `GET /v1/admissions/user/me` (`https://breathecode.herokuapp.com`).
- **Prueba realizada:** consulta autenticada del usuario actual; solicitud hecha con cabecera `Authorization: Token …` (el valor no se registra).
- **Resultado real obtenido:** HTTP 200. La respuesta contenía perfil de usuario; el nombre devuelto fue Arnau Abarca.
- **Estado de funcionamiento:** **funcionó** para validar autenticación y sesión API.

## 2. `4geeks-academico-proyectos`

- **Objetivo:** obtener los proyectos asignados y su estado reportado.
- **Endpoint utilizado:** `GET /v1/assignment/user/me/task` con paginación (`limit=100`, `offset=0` y `offset=100`); filtrado de resultados por `task_type=PROJECT` tras recuperarlos. También se consultó `GET /v1/admissions/academy/cohort/me` para cohortes.
- **Prueba realizada:** se recuperaron las páginas de tareas y se identificaron los elementos de tipo `PROJECT` y sus estados.
- **Resultado real obtenido:** HTTP 200 en las dos páginas de tareas; 145 tareas recuperadas, de las que 26 eran proyectos. De estos, 19 tenían estado `DONE` y 7 `PENDING`. La consulta de cohortes devolvió HTTP 403.
- **Estado de funcionamiento:** **funcionó parcialmente**; lista y estado de proyectos disponibles, pero la consulta auxiliar de cohortes no tuvo permiso. No aparecieron proyectos `APPROVED` en los resultados reportados.

## 3. `4geeks-academico-pendientes`

- **Objetivo:** enumerar tareas pendientes o rechazadas e indicar qué falta completar.
- **Endpoint utilizado:** `GET /v1/assignment/user/me/task` con paginación (`limit=100`, `offset=0` y `offset=100`); resultados filtrados por estado `PENDING` o `REJECTED`. También se consultó `GET /v1/admissions/academy/cohort/me` para cohortes.
- **Prueba realizada:** se revisaron las 145 tareas recuperadas y se clasificaron por estado.
- **Resultado real obtenido:** se contaron 79 tareas `PENDING` y 66 `DONE`; no se informaron tareas `REJECTED`. La consulta de cohortes devolvió HTTP 403. La salida de la prueba incluyó títulos y cohortes en los datos disponibles; no se devolvieron fechas límite en el resumen.
- **Estado de funcionamiento:** **funcionó parcialmente**; se obtuvieron y clasificaron tareas, pero no se pudo verificar cohorte activa y no hubo detalle/feedback adicional de tareas.

## 4. `4geeks-academico-progreso`

- **Objetivo:** resumir el avance mediante estados de tareas, cohorte y actividad académica disponible.
- **Endpoints utilizados:** `GET /v1/admissions/user/me`, `GET /v1/admissions/academy/cohort/me`, `GET /v1/assignment/user/me/task` (paginado) y `GET /v1/activity/me`.
- **Prueba realizada:** autenticación, recuperación de tareas, recuento de estados y consulta de cohortes y actividad.
- **Resultado real obtenido:** usuario HTTP 200; tareas HTTP 200 en ambas páginas, 145 en total: 66 `DONE` y 79 `PENDING`. Cohortes HTTP 403 y actividad HTTP 403. No se obtuvieron métricas de actividad ni total curricular verificable.
- **Estado de funcionamiento:** **funcionó parcialmente**; el recuento de tareas está disponible, pero el resumen no puede confirmar cohorte activa, métricas de actividad ni un porcentaje global de avance.

## Nota de alcance

Los registros describen el resultado de la ejecución de prueba de las llamadas API; no demuestran que las skills se hayan invocado automáticamente como mecanismo separado. La credencial y su valor no se incluyen en este archivo.
