# Laboratorio No. 04: Robótica de Desarrollo, Intro a ROS 2 Jazzy Jalisco - Turtlesim

Este repositorio contiene la solución al Laboratorio No. 04 de la asignatura **Robótica (2026-1)** de la **Universidad Nacional de Colombia**. El objetivo principal es familiarizarse con el ecosistema de **ROS 2 Jazzy Jalisco** sobre **Ubuntu 24.04** utilizando el simulador `turtlesim` y desarrollando nodos de control en Python (`rclpy`).

---

## 👥 Integrantes del Equipo
* **Integrante 1:** Jairo David Diaz Luna - [Correo Electrónico / GitHub]
* **Integrante 2:** [Nombre Completo del Compañero] - [Correo Electrónico / GitHub]

---

## 📝 Descripción General del Laboratorio
[Escribe aquí una descripción. Ejemplo: El laboratorio consiste en el diseño e implementación de un nodo en Python dentro del script `move_turtle.py` (ubicado en el workspace `my_turtle_controller`). Este nodo se encarga de gestionar de forma modular la teleoperación por teclado, la ejecución de trayectorias automáticas y geométricas, el dibujo de iniciales personalizadas y la implementación de un sistema de seguimiento líder-seguidor de dos tortugas].

---

## 🗺️ Diagrama de Flujo (Mermaid)
A continuación se presenta la lógica de funcionamiento del programa, abarcando desde la inicialización del nodo hasta su finalización segura:

```mermaid
graph TD
    A([Inicio del Nodo]) --> B[Inicializar rclpy y crear Clientes/Suscripciones]
    B --> C[/Lectura del Teclado/]
    C --> D{Selección de Acción}
    
    %% Control Manual
    D -- Flechas ↑ ↓ ← → --> E[Control Manual de Velocidad]
    E --> I[Publicar en /turtle1/cmd_vel]
    
    %% Trayectorias Automáticas
    D -- Tecla S / T / A --> F[Trayectoria Automática o Geométrica]
    F --> I
    
    %% Dibujo de Letras
    D -- Teclas Iniciales --> G[Dibujo de Letras Personalizadas]
    G --> I
    
    %% Acciones Complementarias
    D -- Tecla P / R --> H[Servicios: Alternar Lápiz / Reiniciar Posición]
    H --> J[Llamar Servicio Turtlesim]
    
    %% Sistema Líder-Seguidor
    A --> K[Suscribirse a /turtle1/pose y /turtle2/pose]
    K --> L[Calcular Distancia y Orientación Relativa]
    L --> M[Calcular Comandos de Velocidad Progresivos]
    M --> N[Publicar en /turtle2/cmd_vel]
    
    %% Detención y Cierre
    D -- Tecla Q --> O[Detener Movimiento Completamente]
    O --> I
    D -- Ctrl+C / Salida Seguro --> P([Finalización Segura del Programa])
    J --> C
    I --> C


dasdasdasdasdsadassad
