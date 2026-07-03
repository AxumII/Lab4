# Laboratorio No. 04: Robótica de Desarrollo, Intro a ROS 2 Jazzy Jalisco - Turtlesim

[cite_start]Este repositorio contiene la solución al Laboratorio No. 04 de la asignatura **Robótica (2026-1)** de la **Universidad Nacional de Colombia**[cite: 1, 2, 3]. [cite_start]El proyecto implementa el control manual, trayectorias automáticas y un sistema líder-seguidor utilizando nodos en Python con `rclpy` sobre **Ubuntu 24.04** y **ROS 2 Jazzy Jalisco**[cite: 13, 14, 15, 16, 62].

---

## 👥 Integrantes del Equipo
* **Integrante 1:** Jairo David Diaz Luna - [Correo/Usuario de GitHub]
* **Integrante 2:** [Nombre Completo del Compañero] - [Correo/Usuario de GitHub]

---

## 📝 Descripción General del Laboratorio
[Escribe aquí una introducción detallada sobre los objetivos del laboratorio, las herramientas de software utilizadas y el propósito general del paquete `my_turtle_controller` desarrollado en clase].

---

## 🗺️ Diagrama de Flujo (Mermaid)
[cite_start]El siguiente diagrama representa de manera clara la arquitectura lógica y de control de la solución planteada, cumpliendo con los requerimientos mínimos de la guía[cite: 92, 93, 94]:

```mermaid
graph TD
    A([Inicio del Nodo]) --> B[Inicializar rclpy, crear Nodos, Publishers, Subscribers y Clientes de Servicio]
    B --> C[/Lectura Continua del Teclado/]
    B --> D[/Suscripción activa: /turtle1/pose y /turtle2/pose/]
    
    %% Selección de acción por teclado
    C --> E{Selección de Acción}
    
    %% Control Manual
    E -- Flechas Arriba/Abajo/Izquierda/Derecha --> F[Control Manual]
    F --> G[Calcular velocidades lineales/angulares de turtle1]
    
    %% Trayectorias
    E -- Teclas S / T / A --> H[Trayectorias Automáticas]
    H --> I[Calcular geometría o evasión de límites]
    
    %% Letras
    E -- Teclas de Iniciales --> J[Dibujo de Letras]
    J --> K[Calcular coordenadas de las iniciales]
    
    %% Acciones de Servicio
    E -- Teclas P / R --> L[Servicios Turtlesim]
    L --> M[Llamar /turtle1/set_pen o /reset]
    
    %% Detención
    E -- Tecla Q --> N[Detención Completa]
    N --> O[Asignar velocidades a cero]
    
    %% Publicación de Líder
    G --> P[Publicar en /turtle1/cmd_vel]
    I --> P
    K --> P
    O --> P
    
    %% Sistema Líder-Seguidor
    D --> Q[Cálculo del Seguimiento]
    Q --> R[Calcular distancia y orientación relativa entre turtle1 y turtle2]
    R --> S[Publicar comandos de velocidad en /turtle2/cmd_vel]
    
    %% Finalización
    E -- Ctrl+C / Salida del programa --> T([Finalización segura del programa])
    
    %% Ciclos de retorno
    P --> C
    M --> C
    S --> D
🛠️ Explicación de la Solución Implementada1. Control Manual de la TortugaLógica y funciones: [Explica aquí qué métodos utilizaste para capturar el teclado sin bloquear el nodo, y cómo mapeaste las flechas ↑, ↓, ←, → para modificar el tópico /turtle1/cmd_vel sin recurrir a turtle_teleop_key].  2. Funciones Automáticas ImplementadasTecla S (Cuadrado): [Explica la lógica de tiempos, distancias y velocidades angulares usadas para trazar el cuadrado de forma modular].  Tecla T (Triángulo Equilátero): [Detalla el cálculo de los giros de 120° y la velocidad lineal para los 3 lados del triángulo equilátero].  Tecla R (Reiniciar): [Explica qué servicio de turtlesim se llama y cómo limpia la pantalla reposicionando la tortuga].  Tecla P (Lápiz): [Describe el uso del servicio /turtle1/set_pen para activar/desactivar el trazo del dibujo].  Tecla A (Evasión de límites): [Explica matemáticamente cómo detectas los bordes de la ventana usando /turtle1/pose para evitar que la tortuga salga de los límites].  Tecla Q (Detener): [Explica cómo se fuerzan los valores del mensaje Twist a cero de forma inmediata para detener el movimiento].  3. Dibujo de Letras PersonalizadasIniciales del Grupo: [Indica qué letras se escogieron basadas en los nombres de Jairo David Diaz Luna y tu compañero de equipo].  Lógica de dibujo: [Explica paso a paso cómo manipulas las coordenadas angulares y lineales de forma secuencial y no bloqueante para trazar cada letra].  4. Sistema Líder-Seguidor con Dos TortugasCreación de la segunda tortuga: [Explica cómo utilizas el servicio /spawn al arrancar el nodo para crear de manera automática a turtle2].  Algoritmo de seguimiento: [Escribe las fórmulas de distancia euclidiana y ángulo de orientación relativa que calcula el nodo para guiar a turtle2 progresivamente hacia turtle1 basándose en la lectura de sus tópicos de pose].  🔍 Descripción de Componentes ROS 2Nodos Utilizados: [Escribe la lista de nodos propios implementados y del sistema simulado (turtlesim_node)].  Tópicos Utilizados: [Describe tópicos como /turtle1/cmd_vel, /turtle1/pose, /turtle2/cmd_vel, /turtle2/pose, indicando su tipo de mensaje y función].  Servicios Utilizados: [Lista los servicios invocados en la práctica como /spawn, /reset o /turtle1/set_pen].  📺 Evidencias de Ejecución⚠️ Reemplaza los textos ruta/a/la/imagen.png por la ubicación real de tus capturas dentro de la estructura de carpetas del repositorio.Pruebas de Funcionamiento en la SimulaciónMovimiento Manual:Dibujo de Figuras Geométricas (Cuadrado y Triángulo):Dibujo de Letras Personalizadas:Funcionamiento del Sistema Líder-Seguidor:Salidas de Comandos de Inspecciónros2 node listExplicación de lo observado: [Escribe aquí qué indica esta salida y qué nodos se encuentran activos].  Bash# Pega aquí el texto de salida de tu consola
ros2 topic listExplicación de lo observado: [Escribe aquí qué indica esta salida sobre el ecosistema de comunicación actual].  Bash# Pega aquí el texto de salida de tu consola
ros2 topic echo /turtle1/poseExplicación de lo observado: [Escribe aquí qué parámetros de posición, orientación y velocidad lineal/angular se muestran].  Bash# Pega aquí el texto de salida de tu consola
ros2 topic info /turtle1/cmd_velExplicación de lo observado: [Escribe aquí qué indica esta salida sobre el tipo de mensaje y recuento de publishers/subscribers].  Bash# Pega aquí el texto de salida de tu consola
ros2 service listExplicación de lo observado: [Escribe aquí qué indica esta salida sobre los servicios disponibles en turtlesim].  Bash# Pega aquí el texto de salida de tu consola
Visualización de la Arquitectura (rqt_graph)Explicación de las conexiones: [Explica brevemente cómo se relacionan los nodos y tópicos que se ven en tu gráfico de conexiones en tiempo real].  🎥 Video ExplicativoEl análisis del código fuente, los criterios de diseño técnico seleccionados y la demostración en tiempo real de la simulación se pueden visualizar en el siguiente enlace:  📺 [Enlace al video de la sustentación (Máx 10 minutos)]   🎯 ConclusionesConclusión 1: [Escribe un aprendizaje técnico sobre la comunicación por tópicos y el uso de rclpy en ROS 2 Jazzy].  Conclusión 2: [Escribe una conclusión enfocada en los retos de la sincronización líder-seguidor y el manejo no bloqueante de subrutinas].  
