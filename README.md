# Bad Apple!! CLI (Python)

> *Bad Apple!! MV rendered directly in the Command Line Interface (CLI) using ASCII characters in Python.*

[![Python Version](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![CLI Support](https://img.shields.io/badge/Interface-CLI-4D4D4D?style=for-the-badge&logo=windows-terminal&logoColor=white)]()
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)

---

## GIF bien bonito para que se vea acá bien bonito

![Bad Apple Gif](bad_apple_gif.gif)

---

## Tabla de Contenidos
1. [Prefacio](#-prefacio)
2. [Metodología de Desarrollo](#-metodología-de-desarrollo)
3. [Historias de Usuario (Backlog)](#-historias-de-usuario-backlog)
4. [Arquitectura del Proyecto](#-arquitectura-del-proyecto)
5. [Características Principales](#-características-principales)
6. [Requisitos e Instalación](#-requisitos-e-instalación)
7. [Historial de Optimización y Rendimiento](#-historial-de-optimización-y-rendimiento)
8. [Historial de Versiones](#-historial-de-versiones)
9. [Estructura de Funciones](#-estructura-de-funciones)
10. [Problemas Conocidos y Soluciones](#-problemas-conocidos-y-soluciones)
11. [Agradecimientos](#-agradecimientos)

---

## Prefacio

Este proyecto nació como un experimento de fin de semana para compartir entre amigos y ha ido evolucionando a través de iteraciones continuas y aportes de la comunidad.

> ! **Aviso de exención de responsabilidad:** Aunque el código final incluye adaptaciones propias, este proyecto es una amalgama de diversos fragmentos de código recopilados en línea. La idea de reproducir *Bad Apple!!* en la terminal no es novedosa y este repositorio no pretende ser el primero en su tipo, sino una versión optimizada y enfocada en el rendimiento.

► **Demo en video:** Puedes ver la demostración original subida a YouTube [haciendo clic aquí](https://www.youtube.com/watch?v=AZfrXrk3ZHc).

---

##  Metodología de Desarrollo

El proyecto se gestionó bajo un enfoque **Ágil (Iterativo e Incremental)** dividido en sprints cortos para abordar problemas de rendimiento y sincronización:

* **Comunicación & Requerimientos:** Identificación de cuellos de botella (desfasaje de audio, ralentización por E/S en disco) reportados en los Issues de GitHub.
* **Planeación Iterativa:** Priorización del backlog para migrar el procesamiento de almacenamiento físico a memoria RAM y corregir incompatibilidades en Linux.
* **Modelado & Refactorización:** Rediseño del flujo de datos para saltar la creación de archivos temporales `.txt` y procesar directamente arrays de caracteres en RAM.
* **Construcción:** Implementación de multiprocesamiento (`multiprocessing`), temporizadores de alta precisión (`fpstimer`) y reproducción con `pygame`.
* **Cierre & Retrospectiva:** Pruebas de rendimiento en distintas plataformas e integración de soluciones aportadas por colaboradores externos.

---

## Historias de Usuario (Backlog)

Para guiar las funcionalidades clave durante el desarrollo del proyecto, se definieron las siguientes Historias de Usuario (*User Stories*):
```text

| ID | Historia de Usuario | Criterios de Aceptación | Estado |
| :--- | :--- | :--- | :--- |
| **US-01** | **Como** usuario final, **quiero** reproducir la animación de Bad Apple en la consola **para** ver el video musical en formato ASCII. | La animación debe desplegarse fotograma a fotograma directamente en la CLI. | `Completado` |
| **US-02** | **Como** usuario final, **quiero** que el audio esté sincronizado con el video ASCII **para** evitar desfasajes durante la reproducción. | La música debe iniciar a la par con el video y mantenerse precisa usando temporizadores de precisión (`fpstimer`). | `Completado` |
| **US-03** | **Como** desarrollador/usuario, **quiero** que el renderizado procese los fotogramas en RAM **para** eliminar la lentitud por lectura de archivos en disco. | Eliminación de archivos temporales `.txt` procesando la conversión de imágenes directamente en arreglos en memoria. | `Completado` |
| **US-04** | **Como** usuario de Linux/Unix, **quiero** poder ejecutar el proyecto sin errores de reproducción de audio **para** usarlo en cualquier sistema operativo. | Migración de la librería `playsound` a `pygame` para evitar bloqueos del sistema. | `Completado` |
| **US-05** | **Como** usuario avanzado, **quiero** poder especificar cualquier archivo de video propio **para** generar su animación ASCII personalizada. | El programa permite cargar y procesar archivos `.mp4` arbitrarios en la raíz del proyecto (`v4.5`). | `Completado` |

---
```
##  Arquitectura del Proyecto

El sistema sigue un flujo de canalización de procesamiento de video en tiempo real (*Pipeline Pattern*):

```text
┌──────────────┐     ┌──────────────────────┐     ┌─────────────────────┐
│ Archivo MP4  │ ──> │ Extracción de Frames │ ──> │ Redimensionamiento  │
└──────────────┘     │  (OpenCV / FFmpeg)   │     │ & Escala de Grises  │
                     └──────────────────────┘     └─────────────────────┘
                                                             │
                                                             ▼
┌──────────────┐     ┌──────────────────────┐     ┌─────────────────────┐
│ Salida CLI   │ <── │ Sincronización FPS   │ <── │ Mapeo a Caracteres  │
│ (Pantalla)   │     │ (fpstimer + Pygame)  │     │ ASCII en Memoria    │
└──────────────┘     └──────────────────────┘     └─────────────────────┘
