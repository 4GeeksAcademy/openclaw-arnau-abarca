# Skills del proyecto

Este directorio contiene las skills propias de este repositorio. Cada skill vive
en su propia carpeta y tiene `SKILL.md` como documento principal.

## Estructura

```text
skills/
├── README.md
└── <nombre-skill>/
    ├── SKILL.md          # contrato, disparadores y procedimiento
    ├── references/        # criterios y material de consulta, si hace falta
    ├── scripts/           # helpers locales revisados, si hacen falta
    └── assets/            # plantillas o recursos de salida, si hacen falta
```

No crees carpetas vacías: añade `references/`, `scripts/` o `assets/` solo si
la skill realmente necesita esos recursos. Cada `SKILL.md` debe incluir
frontmatter `name` y `description`, distinguir disparador de inputs, especificar
un output comprobable y enlazar cualquier recurso que use. La carpeta de una
skill puede contener solo `SKILL.md` si basta.

## Estado

Documenta primero las skills nuevas y valida su estructura. La documentación de
una skill no activa por sí misma servicios externos ni crea una programación.
Antes de conectarla a servicios externos o programar su ejecución recurrente,
revisa dependencias, permisos, manejo de errores y el alcance concreto de la acción.

## Skills académicas 4Geeks

- `4geeks-academico-autenticar/`: valida el acceso mediante una consulta de solo lectura.
- `4geeks-academico-proyectos/`: lista proyectos y sus estados reportados.
- `4geeks-academico-pendientes/`: detalla tareas pendientes o rechazadas.
- `4geeks-academico-progreso/`: resume estados de tareas y actividad disponible.

Estas skills usan la variable de entorno `TOKEN_4GEEKS` y la cabecera `Authorization: Token …`.
Son procedimientos documentados, todavía no probados contra la API.
