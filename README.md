# PROJECTE
```mermaid
graph TD;
    A[Inicio: Encender sistema] --> B[Menú de configuración: seleccionar modo de entrenamiento]
    B --> C[Generación del estímulo: matriz LED y buzzer]
    C --> D[Medición de tiempo de reacción]
    D --> E[Visualización de resultados en OLED y página web]
    E --> F{Repetir entrenamiento?}
    F -->|Sí| B
    F -->|No| G[Fin]
