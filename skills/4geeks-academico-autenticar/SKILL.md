---
name: 4geeks-academico-autenticar
description: "Cuando se solicite verificar el acceso académico de 4Geeks, valida el token configurado y confirma si la sesión API está activa sin exponer credenciales."
---

# Verificar autenticación académica 4Geeks

## Ejecución

1. Lee la credencial del entorno del proceso desde `TOKEN_4GEEKS`. Esta variable es el nombre real encontrado en `/root/.openclaw/.env`; no uses `Token_4Geeks` como nombre de variable ni leas/imprimas el archivo `.env` directamente.
2. Si la variable falta o está vacía, detente y explica que el proceso de OpenClaw necesita reiniciarse o configurarse para heredarla; nunca muestres el valor.
3. Envía una petición de solo lectura `GET https://breathecode.herokuapp.com/v1/admissions/user/me` con `Authorization: Token <valor>`. No mandes el token a otros destinos ni lo incluyas en logs, errores o salida.
4. Considera válido el token y activa la sesión solo si el endpoint responde correctamente y devuelve datos del usuario con forma válida. Un 401/403 significa que no se ha autenticado; errores de red/servidor son inconclusos, no prueba de token inválido.
5. Devuelve solo resultado (activa, no autenticada o inconclusa) y, si está activo, los campos no sensibles necesarios como nombre y academias/cohortes; no incluyas el token ni datos personales no solicitados.

## Límites

No intentes iniciar sesión ni renovar credenciales: el esquema del cuerpo de `POST /v1/auth/login` no está especificado en la referencia. No realices escrituras ni entregas de tareas en esta skill.
