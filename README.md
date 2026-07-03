# Laboratorio No. 04: Robótica de Desarrollo, Intro a ROS 2 Jazzy Jalisco - Turtlesim

[cite_start]Este repositorio contiene la solución al Laboratorio No. 04 de la asignatura **Robótica (2026-1)** de la **Universidad Nacional de Colombia**[cite: 1, 2, 3]. [cite_start]El objetivo principal es familiarizarse con el ecosistema de **ROS 2 Jazzy Jalisco** sobre **Ubuntu 24.04** utilizando el simulador `turtlesim` y desarrollando nodos de control en Python (`rclpy`)[cite: 3, 13, 14].

---

## 👥 Integrantes del Equipo
* **Integrante 1:** [Nombre Completo] - [Correo Electrónico]
* **Integrante 2:** [Nombre Completo] - [Correo Electrónico]

---

## 📝 Descripción General del Laboratorio
[cite_start]El laboratorio consiste en el diseño e implementación de un nodo en Python dentro del script `move_turtle.py` (ubicado en el workspace `my_turtle_controller`)[cite: 21, 22]. [cite_start]Este nodo se encarga de gestionar de forma modular la teleoperación por teclado, la ejecución de trayectorias automáticas y geométricas, el dibujo de iniciales personalizadas y la implementación de un sistema de seguimiento líder-seguidor de dos tortugas[cite: 22, 33, 44, 51].

---

## 🗺️ Diagrama de Flujo (Mermaid)
[cite_start]A continuación se presenta la lógica de funcionamiento del programa, abarcando desde la inicialización del nodo hasta su finalización segura[cite: 92, 94]:

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



🛠️ Explicación de la Solución Implementada1. Control Manual de la TortugaLógica y funciones: [Explica aquí qué métodos utilizaste para capturar el teclado sin bloquear el nodo, y cómo mapeaste las flechas ↑, ↓, ←, → para modificar el tópico /turtle1/cmd_vel sin recurrir a turtle_teleop_key].  2. Funciones Automáticas ImplementadasTecla S (Cuadrado): [Explica la lógica de tiempos, distancias y velocidades angulares usadas para trazar el cuadrado de forma modular].  Tecla T (Triángulo Equilátero): [Detalla el cálculo de los giros de 120° y la velocidad lineal para los 3 lados del triángulo equilátero].  Tecla R (Reiniciar): [Explica qué servicio de turtlesim se llama y cómo limpia la pantalla reposicionando la tortuga].  Tecla P (Lápiz): [Describe el uso del servicio /turtle1/set_pen para activar/desactivar el trazo del dibujo].  Tecla A (Evasión de límites): [Explica matemáticamente cómo detectas los bordes de la ventana usando /turtle1/pose para evitar que la tortuga salga de los límites].  Tecla Q (Detener): [Explica cómo se fuerzan los valores del mensaje Twist a cero de forma inmediata para detener el movimiento].  3. Dibujo de Letras PersonalizadasIniciales del Grupo: [Indica qué letras se escogieron basadas en los nombres de Jairo David Diaz Luna y tu compañero de equipo].  Lógica de dibujo: [Explica paso a paso cómo manipulas las coordenadas angulares y lineales de forma secuencial y no bloqueante para trazar cada letra].  4. Sistema Líder-Seguidor con Dos TortugasCreación de la segunda tortuga: [Explica cómo utilizas el servicio /spawn al arrancar el nodo para crear de manera automática a turtle2].  Algoritmo de seguimiento: [Escribe las fórmulas de distancia euclidiana y ángulo de orientación relativa que calcula el nodo para guiar a turtle2 progresivamente hacia turtle1 basándose en la lectura de sus tópicos de pose].  🔍 Descripción de Componentes ROS 2Nodos Utilizados: [Escribe la lista de nodos propios implementados y del sistema simulado (turtlesim_node)].  Tópicos Utilizados: [Describe tópicos como /turtle1/cmd_vel, /turtle1/pose, /turtle2/cmd_vel, /turtle2/pose, indicando su tipo de mensaje y función].  Servicios Utilizados: [Lista los servicios invocados en la práctica como /spawn, /reset o /turtle1/set_pen].  📺 Evidencias de Ejecución⚠️ Reemplaza los textos ruta/a/la/imagen.png por la ubicación real de tus capturas dentro de la estructura de carpetas del repositorio.Pruebas de Funcionamiento en la SimulaciónMovimiento Manual:Dibujo de Figuras Geométricas (Cuadrado y Triángulo):Dibujo de Letras Personalizadas:Funcionamiento del Sistema Líder-Seguidor:Salidas de Comandos de Inspecciónros2 node listExplicación de lo observado: [Escribe aquí qué indica esta salida y qué nodos se encuentran activos].  Bash# Pega aquí el texto de salida de tu consola
ros2 topic listExplicación de lo observado: [Escribe aquí qué indica esta salida sobre el ecosistema de comunicación actual].  Bash# Pega aquí el texto de salida de tu consola
ros2 topic echo /turtle1/poseExplicación de lo observado: [Escribe aquí qué parámetros de posición, orientación y velocidad lineal/angular se muestran].  Bash# Pega aquí el texto de salida de tu consola
ros2 topic info /turtle1/cmd_velExplicación de lo observado: [Escribe aquí qué indica esta salida sobre el tipo de mensaje y recuento de publishers/subscribers].  Bash# Pega aquí el texto de salida de tu consola
ros2 service listExplicación de lo observado: [Escribe aquí qué indica esta salida sobre los servicios disponibles en turtlesim].  Bash# Pega aquí el texto de salida de tu consola
Visualización de la Arquitectura (rqt_graph)Explicación de las conexiones: [Explica brevemente cómo se relacionan los nodos y tópicos que se ven en tu gráfico de conexiones en tiempo real].  🎥 Video ExplicativoEl análisis del código fuente, los criterios de diseño técnico seleccionados y la demostración en tiempo real de la simulación se pueden visualizar en el siguiente enlace:  📺 [Enlace al video de la sustentación (Máx 10 minutos)]   🎯 ConclusionesConclusión 1: [Escribe un aprendizaje técnico sobre la comunicación por tópicos y el uso de rclpy en ROS 2 Jazzy].  Conclusión 2: [Escribe una conclusión enfocada en los retos de la sincronización líder-seguidor y el manejo no bloqueante de subrutinas].  
