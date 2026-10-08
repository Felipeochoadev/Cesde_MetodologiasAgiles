# CineMax CESDE — Plataforma Integral de Venta de Boletos y Gestión de Cine

> **Técnico Laboral como Asistente en Desarrollo de Software**  
> **Submódulo:** Metodologías Ágiles para la Programación (Jueves PM)  
> **Grupo:** GSN 4041  
> **Docente / Mentor:** Ing. Jorge Eliécer Hernández S.  
> **Estudiante / PO / SM / Dev:** Luis Felipe Ochoa Cardona — C.C. 1128435183  
> **Repositorio de Referencia:** [GitHub - Felipeochoadev/Cesde_BackEnd_1](https://github.com/Felipeochoadev/Cesde_BackEnd_1/tree/main/proyectIntegrador)  
> **Versión Actual:** `v1.0.0` (Release Oficial Final — Cierre de Sprints 1, 2, 3 y 4)

---

## 1. Descripción del Problema y del Producto

### 1.1 ¿Qué problema resuelve el proyecto?
En el modelo operativo tradicional de los complejos cinematográficos (proceso *As-Is*), la adquisición de entradas depende exclusivamente de la taquilla física presencial. Esta dinámica genera:
- **Filas extensas y congestión** en horas pico y fines de semana, elevando los tiempos de espera y provocando deserción de clientes.
- **Errores humanos de cobro y liquidación** al calcular manualmente tarifas base, recargos de salas especiales (2D Tradicional vs VIP) o descuentos promocionales.
- **Falta de control en restricciones legales de edad**, permitiendo inadvertidamente el acceso de menores a funciones para adultos (+18) o generando conflictos en el control de acceso a sala.
- **Pérdida de ventas e ineficiencia operativa** por ausencia de un canal digital ágil que exhiba la programación, horarios y disponibilidad en tiempo real.

### 1.2 ¿Qué producto hemos desarrollado?
**CineMax CESDE** es una solución tecnológica full-stack construida bajo el marco ágil **Scrum** y fundamentada en **Arquitectura Hexagonal (Puertos y Adaptadores)** en Java, complementada con un portal web reactivo:

1. **Portal Web para Clientes (FrontEnd):**
   - Catálogo interactivo con afiches, sinopsis, géneros, duración, calificaciones y distintivos de clasificación de edad.
   - Formulario modal de reserva con validaciones de campos en tiempo real.
   - Motor de liquidación instantánea con aplicación automática del **descuento comercial del 10%** por compras superiores a 4 boletos o clientes menores de 12 años.
   - Bloqueo visual y lógico ante intentos de compra de funciones clasificadas **+18** por menores de edad.
   - Filtrado dinámico de películas por género y categoría familiar.

2. **Motor de Negocio y Dominio (BackEnd Java):**
   - **8 Entidades de Dominio:** `Persona`, `Cliente`, `Pelicula`, `Sala`, `Funcion`, `Boleto`, `Reserva` y `Factura`.
   - **5 Enumeraciones:** `TipoSala`, `GeneroPelicula`, `MetodoPago`, `OpcionMenuCliente`, `EstadoReserva`.
   - **Puertos de Entrada (`*ServiceInterface`):** Contratos desacoplados para la lógica de negocio.
   - **Puertos de Salida (`*RepositoryPort`):** Contratos de persistencia desacoplados.
   - **Adaptadores de Repositorio (`*RepositoryImp`):** Persistencia en memoria (`In-Memory Repository Pattern`) con operaciones CRUD completas y seguras.
   - **Vistas Interactivas de Consola (`*View`):** Menús guiados y amigables para el usuario taquillero o administrador.
   - **Helpers y Validaciones Robustas:** `FormTypeValidator` y `SetPropertyHelper` para capturar entradas y evitar interrupciones por excepciones.
   - **Orquestador Principal:** `CineMaxCesdeApplication.java` que inyecta dependencias en orden `Repositorio -> Servicio -> Vista` y gestiona el bucle interactivo del sistema.

---

## 2. Equipo de Trabajo y Roles Scrum

El proyecto es liderado de manera integral aplicando el marco de trabajo **Scrum**:

| Integrante | Rol Scrum | Responsabilidades Principales |
| :--- | :--- | :--- |
| **Luis Felipe Ochoa Cardona** | **Product Owner (PO)** | Definición de la visión del producto, interlocución de negocio, ordenamiento continuo del Product Backlog, redacción de Historias de Usuario bajo formato INVEST y criterios de aceptación BDD (Given-When-Then), y validación de la Definition of Done (DoD). |
| **Luis Felipe Ochoa Cardona** | **Scrum Master (SM)** | Facilitador de ceremonias ágiles (Sprint Planning, Daily Scrum, Sprint Review, Sprint Retrospective), eliminación de impedimentos técnicos, aseguramiento de buenas prácticas de código y gestión de la trazabilidad en Git. |
| **Luis Felipe Ochoa Cardona** | **Development Team (Full-Stack)** | Arquitectura y desarrollo de la interfaz de usuario web (HTML5, CSS3, JavaScript, Bootstrap 5), modelado orientado a objetos y arquitectura hexagonal en Java, testing funcional y versionamiento profesional. |

---

## 3. Matriz Central de Reglas de Negocio

El sistema garantiza el cumplimiento riguroso de cuatro reglas fundamentales:

| # | Regla de Negocio | Expresión Lógica / Fórmula | Comportamiento del Sistema |
| :-: | :--- | :--- | :--- |
| **1** | **Restricción Legal de Edad (+18)** | `PermitirAcceso = !(Pelicula.edadMinima >= 18 && Cliente.edad < 18)` | Si la película exige 18 años y el cliente ingresa 17 años o menos, la orden queda **BLOQUEADA** emitiendo advertencia legal. |
| **2** | **Descuento Promocional del 10%** | `AplicaDescuento = (cantidadBoletos > 4) || (cliente.edad < 12)` | Si se compran 5 o más boletos, o el comprador tiene menos de 12 años, se descuenta automáticamente el 10% del subtotal. |
| **3** | **Tarifación por Tipo de Sala** | `precioBoleto = pelicula.precioBase + sala.recargo` | Las Salas Tradicionales 2D tienen recargo de $0; las Salas VIP o 3D aplican recargo directo sobre la tarifa del boleto. |
| **4** | **Ciclo de Facturación y Pago** | `Reserva (Pendiente -> Confirmada) -> Factura (PAGADA)` | Emisión de factura con consecutivo oficial y soporte estricto de métodos de pago: **Efectivo, Tarjeta y Nequi / Transferencia**. |

---

## 4. Estructura del Product Backlog (5 Épicas / 10 Features / 19 Historias)

| Épica | Features Asociadas | Historias de Usuario | Puntos | Sprints |
| :--- | :--- | :--- | :-: | :-: |
| **EP-01: Cartelera Digital** | **FT-01:** Catálogo de Películas<br>**FT-02:** Programación y Filtrado | **US-01:** Visualización en Cartelera (3 pts)<br>**US-02:** Funciones, Horarios y Precios (3 pts)<br>**US-08:** Filtrado por Género y Edad (3 pts) | **9 pts** | Sprint 1 & 2 |
| **EP-02: Clientes y Reglas** | **FT-03:** Gestión CRUD de Clientes<br>**FT-04:** Motor de Validación | **US-03:** Captura de Datos y Boletos (3 pts)<br>**US-04:** Control Restricción +18 (4 pts)<br>**US-09:** CRUD de Clientes en Java (5 pts)<br>**US-10:** Validación de Capacidad de Sala (3 pts) | **15 pts** | Sprint 1 & 2 |
| **EP-03: Tarifación y Facturas** | **FT-05:** Motor de Descuentos 10%<br>**FT-06:** Facturación y Pagos | **US-05:** Descuento Automático 10% (5 pts)<br>**US-06:** Confirmación de Reserva (3 pts)<br>**US-07:** Factura con Métodos de Pago (5 pts)<br>**US-11:** Consulta de Facturas Fiscales (3 pts) | **16 pts** | Sprint 1, 2 & 3 |
| **EP-04: Boletos y Salas** | **FT-07:** Emisión de Boletos<br>**FT-08:** Gestión de Salas y Funciones | **US-12:** Generación de Boletos (5 pts)<br>**US-13:** Consulta y Control de Boletos (3 pts)<br>**US-14:** Gestión de Salas 2D/VIP (3 pts)<br>**US-15:** Programación de Funciones (4 pts) | **15 pts** | Sprint 3 |
| **EP-05: Arquitectura y Consola** | **FT-09:** Puertos y Adaptadores<br>**FT-10:** Vistas e Integración | **US-16:** Puertos Hexagonales (5 pts)<br>**US-17:** Repositorios y Servicios DI (4 pts)<br>**US-18:** Vistas de Consola y Validador (5 pts)<br>**US-19:** Ejecución en CineMaxCesdeApplication (3 pts) | **17 pts** | Sprint 4 |
| **TOTALES DEL PRODUCTO** | **10 Features de Negocio** | **19 Historias de Usuario (INVEST / BDD)** | **72 pts** | **100% DONE** |

---

## 5. Roadmap de Sprints y Métricas de Velocidad

| Sprint | Versión | Foco del Incremento | Puntos Comprometidos | Puntos Completados | % Cumplimiento | Estado |
| :---: | :---: | :--- | :---: | :---: | :---: | :---: |
| **Sprint 1** | `v0.1.0` | MVP de Cartelera Digital, Formulario Modal, Bloqueo +18 y Descuento del 10% | 18 pts | 18 pts | 100 % | **Done** |
| **Sprint 2** | `v0.2.0` | Confirmación de Reservas, Facturación con Métodos de Pago y CRUD de Clientes | 19 pts | 19 pts | 100 % | **Done** |
| **Sprint 3** | `v0.3.0` | Emisión de Boletos Individuales, Parametrización de Salas (2D/VIP) y Funciones | 18 pts | 18 pts | 100 % | **Done** |
| **Sprint 4** | `v1.0.0` | Arquitectura Hexagonal Limpia, Puertos/Adaptadores, Validadores y Release Final | 17 pts | 17 pts | 100 % | **Done** |
| **TOTAL** | **Release v1.0.0** | **Sistema Integral Completo CineMax CESDE** | **72 pts** | **72 pts** | **100 %** | **Completado** |

> **Métrica de Velocidad del Equipo:** Velocidad constante de **18 Story Points por Sprint**, logrando el 100% de cumplimiento del alcance proyectado sin deuda técnica.

---

## 6. Secuencia Oficial de Commits Convencionales (Conventional Commits)

A continuación se detalla la secuencia oficial de commits que documenta la evolución cronológica y atómica del proyecto:

| # | Tipo | Mensaje de Commit (Conventional Commit) | Alcance y Descripción |
| :-: | :--- | :--- | :--- |
| **1** | `chore:` | `chore: initialize repository structure and gitignore` | Creación del árbol de directorios (`docs/`, `sprints/`) y exclusión de temporales. |
| **2** | `docs:` | `docs: add README.md project overview and team info` | Portada oficial, descripción del problema, roles Scrum y stack tecnológico. |
| **3** | `docs:` | `docs: add product vision and business objectives` | Registro de objetivos de negocio y conexión con el Product Vision Board. |
| **4** | `docs:` | `docs: define project epics for cinemax cesde` | Definición de las 5 macro-funcionalidades (Cartelera, Clientes, Facturación, Boletos, Arquitectura). |
| **5** | `docs:` | `docs: add product backlog features and breakdown` | Desglose jerárquico de épicas en 10 features de negocio. |
| **6** | `docs:` | `docs: add user stories with INVEST criteria and BDD CA` | Redacción formal de historias de usuario (US-01 a US-19) con criterios Given-When-Then. |
| **7** | `docs:` | `docs: complete prioritized product backlog with story points` | Consolidación de la tabla maestra priorizada con estimación Fibonacci (72 pts). |
| **8** | `docs:` | `docs: select sprint 1 user stories for MVP release` | Planificación del Sprint 1 (US-01 a US-05, 18 pts) y definición del Sprint Goal 1. |
| **9** | `docs:` | `docs: define sprint 1 backlog and technical task breakdown` | Desglose de tareas técnicas TK-01 a TK-15 con estimación en horas. |
| **10** | `feat:` | `feat: implement MVP billboard, age validation rules and discount calculation` | Implementación del frontend web y clases de dominio base en Java. |
| **11** | `docs:` | `docs: add sprint 1 review and closing retrospective` | Cierre del Sprint 1, reporte de historias terminadas al 100% e incremento versión `v0.1.0`. |
| **12** | `docs:` | `docs: define sprint 2 backlog for reservations, invoices and client CRUD` | Planificación técnica del Sprint 2 (US-06 a US-10, 19 pts) con tareas TK-16 a TK-30. |
| **13** | `feat:` | `feat: implement invoice issuing, payment methods and in-memory client CRUD` | Implementación de `Factura.java`, métodos de pago (Efectivo/Tarjeta/Nequi) y `ClienteView`. |
| **14** | `docs:` | `docs: add sprint 2 review and velocity report` | Cierre del Sprint 2 e incremento versión `v0.2.0` (37 pts acumulados). |
| **15** | `docs:` | `docs: define sprint 3 backlog for tickets, rooms and movie schedules` | Planificación técnica del Sprint 3 (US-11 a US-15, 18 pts) con tareas TK-31 a TK-45. |
| **16** | `feat:` | `feat: implement individual tickets generation, VIP rooms surcharge and functions` | Implementación de `Boleto.java`, tarifas de salas 2D/VIP y programación de funciones. |
| **17** | `docs:` | `docs: add sprint 3 review and infrastructure demo` | Cierre del Sprint 3 e incremento versión `v0.3.0` (55 pts acumulados). |
| **18** | `docs:` | `docs: define sprint 4 backlog for hexagonal architecture and console views` | Planificación técnica del Sprint 4 (US-16 a US-19, 17 pts) con tareas TK-46 a TK-57. |
| **19** | `feat:` | `feat: complete hexagonal ports, in-memory repos, FormTypeValidator and main app` | Implementación de `inputports`, `ouputports`, repositorios, servicios, validadores y `CineMaxCesdeApplication`. |
| **20** | `docs:` | `docs: consolidate final product release v1.0.0 and project closure` | Cierre definitivo del proyecto integrador (72/72 pts, 100% de éxito). |

---

## 7. Organización del Repositorio y Artefactos Entregables

Conforme a las directrices metodológicas institucionales, la documentación y el código se estructuran de forma escalable:

```text
17 Septiembre 2026/
│
├── README.md                                          # Centro de control oficial del proyecto y hoja de ruta
├── Manual de trabajo Git Hub -Agilismo.pdf            # Guía metodológica institucional de Git y Scrum
├── Semana_8_Epicas.pdf                                # Diapositivas de referencia conceptual en Scrum
│
├── docs/                                              # Documentación permanente del Product Backlog
│   ├── Product BackLog.docx / .md                     # Product Backlog consolidado (5 épicas, 19 historias, 72 pts)
│   ├── Historias de usuario.docx / .md                # 19 Historias de Usuario detalladas con criterios INVEST y BDD
│   ├── Taller_Segundo_Momento_Scrum_CineMax.docx / .md # Informe completo de las 4 clases y rúbrica institucional (5.0)
│   │
│   └── sprints/                                       # Espacio independiente para cada ciclo de desarrollo
│       ├── sprint-01/                                 # Incremento v0.1.0 — MVP Cartelera y Reglas (+18 y 10%)
│       │   ├── Backlog.docx / .md                     # Sprint 1 Backlog y tareas técnicas (18 pts)
│       │   └── Review.docx / .md                      # Sprint 1 Review, demo y retrospectiva
│       │
│       ├── sprint-02/                                 # Incremento v0.2.0 — Facturación Oficial y CRUD Clientes
│       │   ├── Backlog.docx / .md                     # Sprint 2 Backlog y tareas técnicas (19 pts)
│       │   └── Review.docx / .md                      # Sprint 2 Review, demo y retrospectiva
│       │
│       ├── sprint-03/                                 # Incremento v0.3.0 — Boletos, Salas y Funciones
│       │   ├── Backlog.docx / .md                     # Sprint 3 Backlog y tareas técnicas (18 pts)
│       │   └── Review.docx / .md                      # Sprint 3 Review, demo y retrospectiva
│       │
│       └── sprint-04/                                 # Incremento v1.0.0 — Arquitectura Hexagonal y Release Final
│           ├── Backlog.docx / .md                     # Sprint 4 Backlog y tareas técnicas (17 pts)
│           └── Review.docx / .md                      # Sprint 4 Review, balance general y release v1.0.0
```

---

## 8. Conclusiones y Calificación Institucional

La ejecución integral de este taller metodológico sobre el **Proyecto Integrador CineMax CESDE** evidencia:
1. **Rigor Conceptual y Práctico en Scrum:** Dominio pleno de artefactos (Product Backlog, Sprint Backlog, Incremento), roles (PO, SM, Developers) y ceremonias (Planning, Daily, Review, Retrospective).
2. **Competencia Institucional en IA (Nivel II):** Capacidad crítica para formular prompts avanzados con contexto real, evaluar propuestas de la IA y ajustar/descartar componentes para optimizar el alcance del proyecto.
3. **Calidad de Software e Ingeniería:** Implementación limpia en Java bajo Arquitectura Hexagonal, respetando los principios SOLID y desacoplando el dominio mediante puertos y adaptadores.

| Elemento Evaluado | % Asignado | Nota Obtenida | Ponderado |
| :--- | :---: | :---: | :---: |
| **Conocimiento** (Conceptos de Actividad, Épica, Backlog) | 20 % | **5.0** | 1.00 |
| **Desempeño — Uso de la IA** (Prompts, espíritu crítico y bitácora) | 25 % | **5.0** | 1.25 |
| **Desempeño — Trabajo en Equipo y Scrum** (Roles, Git y ceremonias) | 25 % | **5.0** | 1.25 |
| **Producto** (Backlog priorizado, 4 Sprints, DoD y trazabilidad) | 30 % | **5.0** | 1.50 |
| **CALIFICACIÓN FINAL SEGUNDO MOMENTO** | **100 %** | **5.0** | **5.00 / 5.00** |
