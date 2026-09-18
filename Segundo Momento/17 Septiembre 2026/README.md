# CineMax CESDE — Plataforma Web de Venta de Boletos y Gestión Integral de Cine

> **Técnico Laboral como Asistente en Desarrollo de Software**  
> **Submódulo:** Metodologías Ágiles (Jueves PM)  
> **Grupo:** GSN 4041  
> **Docente / Mentor:** Ing. Jorge Eliécer Hernández S.  
> **Estudiante:** Luis Felipe Ochoa Cardona — C.C. 1128435183  
> **Repositorio de Referencia:** [GitHub - Felipeochoadev](https://github.com/Felipeochoadev/Cesde_BackEnd_1/tree/main/proyectIntegrador)  
> **Versión Actual:** \V0.1.0\ (Cierre de Sprint 1)

---

## 1. Descripción del Problema y del Producto

### 1.1 ¿Qué problema resuelve el proyecto?
En el modelo operativo tradicional de las salas de cine (proceso *As-Is*), la venta de entradas depende exclusivamente de la taquilla física. Esta dinámica genera:
- **Filas extensas y congestión** en horas pico y fines de semana.
- **Errores humanos de cobro y liquidación** al calcular precios base, recargos de salas especiales (VIP, 2D) o descuentos promocionales.
- **Falta de control en restricciones de edad**, permitiendo inadvertidamente el ingreso de menores a funciones para mayores de edad (+18) o generando reclamos en puerta.
- **Pérdida de ventas** por falta de un canal digital ágil que exhiba la disponibilidad y horarios en tiempo real.

### 1.2 ¿Qué producto estamos desarrollando?
**CineMax CESDE** es una solución tecnológica full-stack diseñada bajo arquitectura limpia y modular que moderniza la operación del cine:
1. **Portal Web para Clientes (FrontEnd):** Catálogo visual de películas en cartelera con imágenes, sinopsis, duración, horarios y clasificación; formulario interactivo de reserva de boletos con validaciones en vivo; aplicación automática de reglas de negocio (descuento del 10% por compra mayor a 4 boletos o menores de 12 años, bloqueo estricto de películas +18 para menores de edad).
2. **Motor de Dominio y Negocio (BackEnd Java):** Conjunto de entidades orientadas a objetos (\Persona\, \Cliente\, \Pelicula\, \Sala\, \Funcion\, \Boleto\, \Reserva\, \Factura\) capaces de gestionar la programación de salas, liquidar tarifas con precisión matemática y emitir comprobantes de pago detallados.

---

## 2. Equipo de Trabajo y Roles Scrum

El proyecto es liderado de manera integral aplicando el marco de trabajo **Scrum**:

| Integrante | Rol Scrum | Responsabilidades Principales |
| :--- | :--- | :--- |
| **Luis Felipe Ochoa Cardona** | **Product Owner (PO)** | Definición de la visión del producto, priorización y ordenamiento del Product Backlog, redacción de Historias de Usuario con criterios de aceptación e interlocución de negocio. |
| **Luis Felipe Ochoa Cardona** | **Scrum Master (SM)** | Facilitador de ceremonias ágiles (Planning, Daily, Review, Retrospective), remoción de impedimentos, aseguramiento de los principios ágiles y control de calidad. |
| **Luis Felipe Ochoa Cardona** | **Development Team (Full-Stack)** | Arquitectura y desarrollo de la interfaz de usuario web (HTML, CSS, JS, Bootstrap), programación del modelo de dominio en Java (POO), testing funcional y versionamiento en Git. |

---

## 3. Tecnologías Utilizadas

### Frontend
- **HTML5 Semántico:** Estructuración accesible de la cartelera, tarjetas de películas y formularios modales de compra.
- **CSS3 & Bootstrap 5:** Diseño visual moderno, modo oscuro cinematográfico y maquetación 100% responsiva para dispositivos móviles, tablets y escritorio.
- **JavaScript:** Lógica reactiva en cliente, validaciones de formularios en tiempo real, manipulación dinámica del DOM y cálculo instantáneo de subtotales y descuentos.

### Backend
- **Java:** Lenguaje robusto orientado a objetos para el modelado del dominio y la ejecución de reglas de negocio.
- **Apache Maven:** Gestión de dependencias, ciclo de vida del proyecto y compilación.
- **Arquitectura Modular por Capas:** Separación de responsabilidades en paquetes: \domain\, \
epository\, \service\, \view\, y \main\ (\App.java\).

### Metodologías, Control de Versiones y Gestión
- **Git & GitHub:** Control de versiones distribuido, convención de *Conventional Commits* y flujo de trabajo en la rama main.
- **Scrum:** Ciclos iterativos de 2 semanas, épicas, features, historias de usuario.

---

## 4. Organización del Repositorio

Siguiendo las directrices del **Manual de Trabajo Scrum** la documentación y el código se organizan de forma escalable y estandarizada:

> **Regla de Oro Metodológica:**
> 1. Existe **un solo Product Backlog** permanente que evoluciona durante todo el ciclo de vida del producto (\docs/product-backlog.\).
> 2. Cada Sprint cuenta con su **propio espacio independiente** (\docs/sprints/sprint-01/\, \docs/sprints/sprint-02/\, etc.) con su respectivo \sprint-backlog\ y \sprint-review\.

---

## 5. Estrategia de Ramas en Git

Para garantizar un flujo de integración continuo y ordenado, el proyecto se hace en la rama principal ya que soy un unico integrante:


- **\main\:** Contiene las versiones estables y liberables del producto al final de cada Srprint

---

## 6. Convención y Secuencia de Commits (Sprint 1)

Los cambios se registran mediante mensajes atómicos, claros y estandarizados A continuación se detalla la secuencia oficial de commits ejecutada durante el Sprint 1:

| # | Tipo de Commit | Mensaje de Commit | Descripción del Avance |
| :-: | :--- | :--- | :--- |
| **1** | \chore:\ | \chore: initialize repository structure and gitignore\ | Creación del árbol de directorios (\docs/\, \sprints/\) y exclusión de temporales. |
| **2** | \docs:\ | \docs: add README.md project overview and team info\ | Portada completa, descripción del problema, roles y tecnologías. |
| **3** | \docs:\ | \docs: add product vision and business objectives\ | Registro de los objetivos del negocio y conexión con el Product Vision Board. |
| **4** | \docs:\ | \docs: define project epics for cinemax cesde\ | Definición de las 5 macro-funcionalidades (Cartelera, Reservas, Tarifación, Asientos, Admin). |
| **5** | \docs:\ | \docs: add product backlog features and breakdown\ | Desglose de épicas en features concretas de negocio. |
| **6** | \docs:\ | \docs: add user stories with INVEST criteria and BDD CA\ | Redacción formal de historias de usuario (US-01 a US-10) con criterios de aceptación. |
| **7** | \docs:\ | \docs: complete prioritized product backlog with story points\ | Consolidación de la tabla del Product Backlog priorizada con estimación Fibonacci. |
| **8** | \docs:\ | \docs: select sprint 1 user stories for MVP release\ | Selección de historias prioritarias (US-01 a US-05, 18 pts) para el Sprint 1. |
| **9** | \docs:\ | \docs: define sprint 1 backlog and technical task breakdown\ | Planificación técnica del Sprint 1, tareas en horas y asignación de responsabilidades. |
| **10** | \Feat:\ | \Feat: implement MVP billboard, age validation rules and discount calculation\ | Implementación funcional del código base en frontend y clases de dominio Java. |
| **11** | \docs:\ | \docs: add sprint 1 review and closing retrospective\ | Cierre del sprint, reporte de historias terminadas al 100% e incremento versión \V0.1.0\. |

---
