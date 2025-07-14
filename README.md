# Sistema de Entrenamiento de Respuesta a Estímulos (ESP32‑S3)

> **Autors:** Marc Grau Casado
> **Asignatura:** Procesadores Digitales (curso 2025‑2026)

---

## 📑 Descripción

Sistema interactivo basado en **ESP32‑S3** que mide y mejora el tiempo de reacción del usuario mediante estímulos visuales (matriz LED 8×8), sonoros (buzzer) y táctiles (pulsadores / sensores IR).
El dispositivo muestra los resultados en una **pantalla OLED 128×64** y publica un **ranking** persistente a través de un **servidor web local** (ESPAsyncWebServer) en modo *Access Point*.

---

## 🎯 Funcionalidades

* **Tres niveles de dificultad** (fácil, medio, difícil) con parametrización del intervalo de estímulos.
* **Estímulos aleatorios** combinando matriz LED y sonido.
* **Medición precisa** del tiempo de reacción y cálculo automático de la puntuación.
* **Visualización en OLED** y **ranking histórico persistente** (LittleFS / SD opcional).
* **Interfaz web** para consultar estadísticas desde cualquier dispositivo conectado al punto de acceso Wi‑Fi.
* Soporte multijugador y reinicio rápido del juego.

---

## 🖼️ Diagrama de bloques

*Inserta aquí la imagen `diagrama_bloques.png` o similar.*

```
┌────────┐      ┌────────────┐      ┌──────────┐
│Matriz  │      │  ESP32‑S3  │      │ Pantalla │
│ LED 8×8│◀────▶│(CPU + Wi‑Fi)│────▶│  OLED    │
└────────┘      └────────────┘      └──────────┘
     ▲                ▲  ▲                ▲
     │                │  │                │
┌─────────┐        ┌───┴───┐          ┌────┴────┐
│Buzzer   │        │Pulsador│          │  Web    │
└─────────┘        │/Sensor │          │Cliente  │
                   └────────┘          └─────────┘
```

---

## 💸 Cálculo de costes

| Componente             | Cantidad | Precio (EUR) |
| ---------------------- | :------: | -----------: |
| ESP32‑S3               |     1    |          6 € |
| Pantalla OLED 128×64   |     1    |          7 € |
| Buzzer                 |     4    |          6 € |
| Pulsadores             |    10    |          9 € |
| Sensores IR            |     6    |          6 € |
| PCB doble cara 21 × ?? |     1    |         15 € |
| Protoboard             |     2    |          6 € |
| Tabla de madera        |     1    |         25 € |
| Rollo de estaño        |     1    |          8 € |
| Soldador (herramienta) |     1    |          0 € |
| **Total aproximado**   |          |     **88 €** |

---

## 🔄 Flujo de funcionamiento

1. **Inicio** – encendido del sistema.
2. **Menú** – selección de modo/dificultad en la OLED mediante pulsadores.
3. **Generación de estímulo** – activación matriz LED + buzzer.
4. **Medición** – una vez empieza el modo de juego hay una cuenta atrás de 5s y empieza el juego. El ESP32‑S3 cronometra la respuesta de reacción. Se ha añadido que por cada tres fallos cometidos, se bajará un punto de la nota final máxima.
5. **Resultados** – se muestra la nota final durante 15s y luego te da la opción de elegir si quieres repetir el juego indicando que modo (45s). Si no se elige nada se apaga automaticamente. Las 3 mejores notas junto con sus tiempos se mostraran en el ranking de la página web.

---

## 🔧 Componentes principales

| Módulo                       | Función                                                                |
| ---------------------------- | ---------------------------------------------------------------------- |
| **ESP32‑S3**                 | CPU, Wi‑Fi AP, lógica de juego, cronómetro, almacenamiento LittleFS/SD |
| **Matriz LED 8×8**           | Estímulos visuales                                                     |
| **Buzzer**                   | Estímulos sonoros                                                      |
| **Pulsadores / Sensores IR** | Entrada del usuario, selección de dificultad                           |
| **Pantalla OLED**            | Menús y resultados                                                     |
| **Servidor Web**             | Estadísticas y ranking remoto                                          |

---

## 🚀 Puesta en marcha

```bash
# Clonar proyecto (privado)
$ git clone https://github.com/tuusuario/stimulus-trainer.git
$ cd stimulus-trainer

# Instalar PlatformIO y compilar
$ pio run

# Flashear al ESP32‑S3 (ajusta el puerto serie)
$ pio run -t upload --upload-port /dev/ttyUSB0
```

> ⚠️ Reemplaza las credenciales Wi‑Fi por valores genéricos en `config.h` antes de publicar el repo.

---

## 📁 Estructura del repositorio

```
├── src/            # Código fuente (main.cpp, handlers, utils…)
├── lib/            # Librerías propias (si aplica)
├── data/           # Archivos LittleFS (ranking.json, html, css)
├── docs/           # Memoria PDF, diagrama de bloques, fotos
├── platformio.ini  # Configuración de PlatformIO
└── README.md       # Este documento
```

---

## 📈 Resultados esperados

* Tiempo medio de reacción en población general \~200 ms.
* Puntuaciones objetivo: **8 (fácil)** · **6 (normal)** · **4 (difícil)**.
* Cada incremento de dificultad reduce la puntuación en ≈2 puntos.


