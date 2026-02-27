# ORM – Sistema de Gestión Académica

```mermaid
erDiagram

    PERSONA {
        int id_persona PK
        string nombres
        string apellidos
        string cedula
        string correo
    }

    ESTUDIANTE {
        int id_persona PK
        string carrera
        int semestre
    }

    DOCENTE {
        int id_persona PK
        string especialidad
        string tipo_contrato
    }

    MATERIA {
        int id_materia PK
        string nombre
        int creditos
        string carrera
        int semestre
    }

    MATRICULA {
        int id_matricula PK
        string periodo
        date fecha_matricula
        int id_estudiante
        int id_materia
    }

    CALIFICACION {
        int id_calificacion PK
        float nota1
        float nota2
        float nota_final
        string estado
        int id_matricula
    }

    PERSONA ||--o{ ESTUDIANTE : es
    PERSONA ||--o{ DOCENTE : es

    ESTUDIANTE ||--o{ MATRICULA : realiza
    MATERIA ||--o{ MATRICULA : incluye

    MATRICULA ||--o| CALIFICACION : genera
```

## Restricciones Externas

1. Especialización total:
   Toda PERSONA debe ser ESTUDIANTE o DOCENTE.

2. Regla de negocio:
   Si nota_final >= 7 → estado = "Aprobado"
   Si nota_final < 7 → estado = "Reprobado"