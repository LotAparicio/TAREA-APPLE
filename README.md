# Bad Apple!! CLI (Python)

> *Bad Apple!! MV rendered directly in the Command Line Interface (CLI) using ASCII characters in Python.*

[![Python Version](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![CLI Support](https://img.shields.io/badge/Interface-CLI-4D4D4D?style=for-the-badge&logo=windows-terminal&logoColor=white)]()
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)

---

## Preview

![Bad Apple Gif](bad_apple_gif.gif)

---

## Tabla de Contenidos
1. [Descripción del Proyecto](#descripción-del-proyecto)
2. [Selección de Metodología de Desarrollo](#selección-de-metodología-de-desarrollo)
3. [Historias de Usuario (User Stories)](#historias-de-usuario-user-stories)
4. [Arquitectura del Proyecto](#arquitectura-del-proyecto)
5. [Instrucciones de Ejecución](#instrucciones-de-ejecución)
6. [Historial de Optimización y Rendimiento](#historial-de-optimización-y-rendimiento)
7. [Historial de Versiones](#historial-de-versiones)
8. [Problemas Conocidos y Soluciones](#problemas-conocidos-y-soluciones)
9. [Retrospectiva del Proyecto - Práctica 1](#retrospectiva-del-proyecto---práctica-1)
10. [Agradecimientos & Créditos](#-agradecimientos--créditos)

---

## Descripción del Proyecto

Este proyecto es una aplicación modular basada en CLI desarrollada en Python para la extracción, procesamiento, conversión y renderizado en tiempo real del video musical **Bad Apple!!** en formato ASCII dentro de la terminal de comandos.

### Justificación de la Necesidad
Elegimos este proyecto porque responde al reto técnico de optimizar el procesamiento multimedia en consola. Desde la perspectiva de la Ingeniería de Software, abordar este problema permite explorar y resolver cuellos de botella reales de entrada/salida (I/O) en disco, sincronización de hilos y procesos en paralelo, y gestión eficiente de memoria RAM para gráficos en tiempo real.

> **Aviso de exención de responsabilidad:** Aunque el código final incluye adaptaciones propias, este proyecto es una amalgama de diversos fragmentos de código recopilados en línea. La idea de reproducir *Bad Apple!!* en la terminal no es novedosa; este repositorio se enfoca en el análisis, refactorización y optimización de rendimiento.

**Demo en video:** Puedes ver la demostración original subida a YouTube [haciendo clic aquí](https://www.youtube.com/watch?v=AZfrXrk3ZHc).

---

## Selección de Metodología de Desarrollo

### Enfoque Seleccionado: Metodología Ágil (Kanban)

**Justificación:**
1. **Duración y Flexibilidad:** Dado el marco de tiempo reducido de la práctica, un enfoque ágil nos permite trabajar con entregas incrementales y priorizar los módulos del sistema (audio, procesamiento de imágenes, sincronización FPS) de forma independiente.
2. **Estructura Modular:** Al estar el proyecto dividido en componentes individuales (extracción de cuadros, renderizado ASCII, barra de progreso), Kanban facilita asignar cada funcionalidad mediante *Issues* en GitHub Projects.
3. **Adaptabilidad:** Permite ajustar los requisitos y resolver fallos detectados durante las pruebas (como el desfasaje de tiempo o bloqueos en Linux) sin romper la planificación general.

---

## Historias de Usuario (User Stories)

* **HU-01: Extracción y Procesamiento de Video**
  * **Como** usuario del sistema,
  * **Quiero** descomponer un archivo de video `.mp4` en fotogramas secuenciales,
  * **Para** prepararlos para su posterior conversión a formato ASCII.

* **HU-02: Conversión Gráfica a ASCII**
  * **Como** desarrollador del motor gráfico,
  * **Quiero** transformar cada fotograma a escala de grises y mapear los niveles de brillo a caracteres de texto,
  * **Para** generar la representación visual en la terminal.

* **HU-03: Sincronización de Audio y Frecuencia de Cuadros (FPS)**
  * **Como** usuario final,
  * **Quiero** que la reproducción del audio coincida de manera exacta con el renderizado visual,
  * **Para** evitar acumulaciones de retraso (drift) durante la animación.

* **HU-04: Optimización y Manejo en Memoria RAM**
  * **Como** administrador del sistema,
  * **Quiero** procesar las matrices ASCII directamente en memoria omitiendo archivos `.txt` en almacenamiento físico,
  * **Para** eliminar el cuello de botella de E/S (I/O) y reducir los tiempos de carga previos a 10-15 segundos.

---

## Arquitectura del Proyecto

```text
.
├── bad-apple/
│   ├── modules/              # Módulos de procesamiento (ASCII, audio, video)
│   │   ├── ascii_generator.py # Conversión de píxeles a caracteres ASCII
│   │   ├── audio_player.py    # Motor de audio con Pygame
│   │   └── utils.py           # Generador de barra de progreso
│   ├── assets/                # Archivos multimedia (MP4, GIF)
│   ├── touhou_bad_apple_v4.0.py # Motor ejecutable principal (RAM optimized)
│   ├── requirements.txt       # Lista de dependencias del proyecto
│   └── README.md              # Documentación del repositorio
---
