---
name: daily-founder-quote
description: "Prepara y envía a Arnau un email con una cita auténtica sobre emprendimiento en inglés o español, atribuida a su autor y firmada por Nadador."
metadata:
  status: implemented
  version: 1.0.0
---

# Cita diaria sobre emprendimiento

## Propósito

Preparar un email para `arnau@foodizon.io` con una cita real relacionada con el
emprendimiento, en inglés o español, conservando el idioma original de la cita.
El cuerpo incluirá solo la cita, su autor y la firma `Nadador`; no añadirá
comentarios ni una reflexión.

## Disparador e inputs

- **Disparador previsto:** una automatización externa la invoca cada día a las
  08:30 en `Europe/Madrid`. La hora es el disparador, no un input que el usuario
  tenga que proporcionar al invocarla.
- **Inputs de ejecución:** fecha local del envío; destinatario, asunto,
  idiomas permitidos, formato y firma son valores fijos definidos abajo. La
  automatización debe proporcionar la fecha local al invocar la skill.
- No se debe inferir el idioma de la cita a partir de una traducción: solo se
  admiten citas cuya formulación original pueda verificarse en inglés o español.

## Procedimiento de ejecución

1. Comprueba que hay una herramienta de búsqueda web autorizada y disponible.
   Busca una cita pertinente y verifica el texto original y su atribución en
   una fuente primaria o una referencia editorial fiable. Sigue
   [`references/quote-sourcing.md`](references/quote-sourcing.md). Si no puedes
   verificar ambos, detente sin enviar y explica el bloqueo.
2. Usa solo citas originalmente en inglés o español. Conserva la formulación
   original; no traduzcas citas de otros idiomas. Si hay un historial accesible
   de citas usadas, evita repeticiones recientes; si no lo hay, no afirmes que
   la cita es nueva o no repetida.
3. Prepara un cuerpo en texto plano con exactamente la cita, el autor y la
   firma `Nadador`, sin introducción, reflexión, enlace ni texto adicional.
4. Antes de enviar, comprueba que el destinatario es `arnau@foodizon.io`, el
   asunto es `tu frase motivacional diaria` y el cuerpo cumple el formato.
5. Envía usando la acción Gmail de Zapier indicada abajo, solo cuando la
   autorización para ese envío esté vigente. Si la llamada falla o su resultado
   es incierto, no afirmes que se envió y no reintentes hasta comprobar estado.
6. Informa si el envío se confirmó o si quedó bloqueado/falló. No incluyas una
   cita sin fuente fiable como si fuera auténtica.

## Acción de correo disponible

Se inspeccionó que Zapier ofrece la acción de Gmail para enviar correo y que
hay una conexión predeterminada disponible. No se realizó un envío de prueba;
no se afirma que el flujo de extremo a extremo esté verificado. Usa esa
conexión de Gmail disponible en Zapier; no incluyas IDs de conexión ni
credenciales en esta skill. Antes de invocarla, vuelve a inspeccionar el
esquema de la acción y comprueba que los campos siguen disponibles.

- Acción: `ZapierAction[GoogleMailV2CLIAPI:message]`
- Tool: `execute_zapier_write_action`, `tool_name: gmail_send_email`
- Valores fijos: `to: ["arnau@foodizon.io"]`,
  `subject: "tu frase motivacional diaria"`, `body_type: "plain"`.
- Valor calculado tras verificar la cita: `body` con el texto exacto de la
  cita, su autor y `Nadador` como firma.
- No añadas CC, BCC, adjuntos, firmas automáticas ni destinatarios adicionales.

## Output esperado

- Un email dirigido a `arnau@foodizon.io`.
- Cuerpo, sin texto adicional:

  ```text
  “Texto de la cita” — Autor

  Nadador
  ```

- Asunto: `tu frase motivacional diaria`.
- Resultado comprobable: confirmación de envío de la integración, o un error
  explícito sin afirmar que el email se envió.

## Estado y límites

Esta skill define el procedimiento bajo demanda; no se ejecuta por el mero
hecho de que sean las 08:30. La programación diaria a las 08:30
`Europe/Madrid` es una automatización separada y no se ha creado aquí. Para
activarla, configura un disparador recurrente autorizado que invoque este
procedimiento, limita sus permisos al buscador web y a la acción de envío de
Gmail descrita arriba, y verifica su estado antes de considerar el envío
operativo. No envíes un email de prueba sin autorización.
