# Tarea #5: Análisis de Trade-offs en un Proyecto de Software

**Universidad de San Carlos de Guatemala**
**Facultad de Ingeniería – Escuela de Ingeniería en Ciencias y Sistemas**
**Laboratorio de Comunicación Asertiva – Sección A – Segundo Semestre 2026**

## Integrantes

| No. | Nombre | Rol en el análisis |
|-----|--------|--------------------|
| 1 | Hans Alexander Juárez Cano  202501149| Líder técnico / facilitador de la negociación |
| 2 | Miguel Tomás López Nix| Analista de calidad y riesgos |
| 3 | Hassan Alfredo Antony Lopez Guarchaj | Analista de costos y planificación |

---

## Índice

1. [Planteamiento del problema](#1-planteamiento-del-problema)
2. [Identificación de trade-offs](#2-identificación-de-trade-offs)
3. [Análisis de alternativas](#3-análisis-de-alternativas)
4. [Negociación técnica](#4-negociación-técnica)
5. [Decisión final](#5-decisión-final)
6. [Reflexión](#6-reflexión)

---

## 1. Planteamiento del problema

### 1.1 Descripción del problema

El equipo desarrolla **"PedidoYa Local"**, una aplicación web para que pequeños negocios de comida de Guatemala reciban pedidos por internet, administren su inventario básico y notifiquen el estado del pedido al cliente. A tres semanas de la fecha de entrega del primer release, el equipo detecta que **el alcance planificado no cabe en el tiempo disponible** si se pretende mantener el nivel de calidad acordado.

El problema central es un **conflicto entre tiempo, calidad y alcance**: se debe decidir qué se sacrifica o se pospone para entregar un producto funcional y confiable en la fecha comprometida.

### 1.2 Contexto del proyecto

| Elemento | Detalle |
|----------|---------|
| Proyecto | PedidoYa Local (aplicación web de pedidos para negocios pequeños) |
| Cliente | Dueño de un negocio de comida rápida que usará el sistema en producción |
| Metodología | Scrum simplificado, sprints de 1 semana |
| Estado actual | Fin del sprint 3 de 6 |
| Funcionalidades completas | Registro/inicio de sesión, catálogo de productos, carrito de compras |
| Funcionalidades pendientes | Pasarela de pago, notificaciones por WhatsApp/correo, panel de administración, reportes de ventas, módulo de inventario |
| Tecnologías | Frontend web, API REST, base de datos relacional |
| Riesgo principal | Entregar tarde, o entregar a tiempo con errores en el flujo de pedidos y pagos |

### 1.3 Restricciones

| Tipo | Restricción |
|------|-------------|
| **Tiempo** | 3 semanas restantes; fecha de entrega fija e inamovible (compromiso con el cliente) |
| **Equipo** | 3 desarrolladores estudiantes, con ~12 horas semanales cada uno por la carga de otros cursos (~108 horas totales disponibles) |
| **Costo** | Presupuesto prácticamente nulo: solo capas gratuitas de servicios en la nube |
| **Alcance** | El cliente considera indispensables: pedidos, pagos y notificaciones |
| **Experiencia** | Ningún integrante ha integrado antes una pasarela de pagos real ni ha implementado pruebas automatizadas a gran escala |
| **Calidad** | Un error en pedidos o cobros afecta directamente los ingresos del cliente y la confianza en el sistema |

### 1.4 Estimación del problema

| Concepto | Horas |
|----------|-------|
| Horas disponibles (3 semanas) | -108 |
| Horas necesarias para el alcance completo con pruebas | -165 |
| **Déficit** | **-57 horas** |

Existe una brecha de aproximadamente un tercio de la capacidad del equipo, por lo que **no se puede cumplir todo**; es necesario decidir con criterios técnicos.

---

## 2. Identificación de trade-offs

| # | Trade-Off | Opción A | Opción B |
|---|-----------|----------|----------|
| 1 | Rapidez vs. calidad | Entregar rápido, con pruebas manuales mínimas | Invertir tiempo en pruebas automatizadas y revisión de código |
| 2 | Costo vs. funcionalidad | Construir todas las funcionalidades desde cero | Usar servicios de terceros (pasarela de pago y autenticación) y reducir el alcance a un MVP |
| 3 | Simplicidad vs. escalabilidad | Arquitectura monolítica simple | Arquitectura de microservicios preparada para crecer |
| 4 | Alcance completo vs. entrega incremental | Entregar todo el alcance en un solo release | Entregar un MVP ahora y el resto en una segunda versión |

---

## 3. Análisis de alternativas

### 3.1 Trade-off 1: Rapidez vs. calidad

**Opción A: Entregar rápido con pruebas manuales mínimas**

- **Explicación:** el equipo dedica casi todo el tiempo a programar funcionalidades y solo realiza pruebas manuales al final.
- **Ventajas:**
  - Mayor cantidad de funcionalidades terminadas.
  - Cumple la fecha con apariencia de completitud.
- **Desventajas:**
  - Alta probabilidad de errores en el flujo de pedidos y pagos.
  - Los defectos se descubren tarde, cuando corregirlos es más costoso.
  - Deuda técnica que dificulta futuras mejoras.
- **Impacto en el proyecto:** riesgo alto de que el cliente encuentre fallos en producción, lo que daña la confianza y obliga a trabajo urgente posterior.

**Opción B: Pruebas automatizadas y revisión de código**

- **Explicación:** se destina cerca del 20 % del tiempo a pruebas automatizadas de los flujos críticos (pedido, pago, notificación) y revisión de código entre pares.
- **Ventajas:**
  - Detecta errores temprano, cuando son más baratos de corregir.
  - Da confianza para modificar código sin romper lo existente.
  - Mejora la calidad percibida por el cliente.
- **Desventajas:**
  - Consume horas que se restan al desarrollo de funcionalidades.
  - Requiere aprender herramientas de prueba (curva de aprendizaje).
- **Impacto en el proyecto:** se entregan menos funcionalidades, pero las entregadas son confiables.

### 3.2 Trade-off 2: Costo vs. funcionalidad

**Opción A: Construir todo desde cero**

- **Explicación:** desarrollar autenticación, pagos y notificaciones de forma propia.
- **Ventajas:**
  - Control total del código.
  - Sin dependencia de terceros ni de sus límites.
- **Desventajas:**
  - Muy alto consumo de horas en componentes que no son el valor diferencial del producto.
  - Los componentes de seguridad y pagos desarrollados sin experiencia aumentan el riesgo.
- **Impacto en el proyecto:** agrava el déficit de horas y compromete la fecha de entrega.

**Opción B: Usar servicios de terceros y reducir alcance a un MVP**

- **Explicación:** se integra una pasarela de pagos y un servicio de autenticación existentes (capas gratuitas) y se limita el alcance a lo indispensable.
- **Ventajas:**
  - Reduce significativamente las horas de desarrollo.
  - Los proveedores ya cuentan con seguridad y cumplimiento probados.
- **Desventajas:**
  - Dependencia del proveedor y de sus condiciones (límites, comisiones).
  - Menor personalización.
  - Requiere tiempo de aprendizaje de la API.
- **Impacto en el proyecto:** libera tiempo para pruebas y para el flujo principal; el costo monetario es bajo o nulo en esta etapa.

### 3.3 Trade-off 3: Simplicidad vs. escalabilidad
**Opción A**: Monolito simple
**Explicación:** una sola aplicación y una sola base de datos, organizada en módulos internos.
**Ventajas:**
- Rápido de desarrollar, probar y desplegar.
- Menor complejidad operativa para un equipo de 3 personas.
- Suficiente para el rango esperado de un negocio pequeño.
**Desventajas:**
- Realizar partes específicas por separado es más difícil.
- Si crece mucho, puede requerir refactorización.
**Impacto en el proyecto:** permite concentrar el esfuerzo en las funcionalidades y no en la infraestructura.
**Opción B:** Microservicios
**Explicación:* separar pedidos, pagos, notificaciones e inventario en servicios independientes.
**Ventajas:**
- Escalabilidad independiente por servicio.
- Facilita que equipos distintos trabajen en paralelo a futuro.
**Desventajas:**
- Mayor complejidad de despliegue, comunicación entre servicios y monitoreo.
- Aumenta de forma notable el trabajo de configuración.
- Excesivo para un equipo pequeño y un volumen bajo de usuarios.
**Impacto en el proyecto:** probablemente consumiría gran parte de las horas restantes sin aportar valor visible al cliente en este release.

  ### 3.4 Trade-off 4: Alcance completo vs. entrega incremental

**Opción A: Entregar todo el alcance en un solo release**

**Explicación:** intentar completar las cinco funcionalidades pendientes antes de la fecha.
**Ventajas:**

  * El cliente recibe el producto "completo".
**Desventajas:**

  * Con un déficit de \-57 horas, implica recortar calidad, trabajar sin descanso o incumplir la fecha.
  * Riesgo de agotamiento del equipo.
**Impacto en el proyecto:** alta probabilidad de entrega tardía o con defectos.

**Opción B: Entregar un MVP y planificar una segunda versión**

**Explicación:** el primer release incluye solo lo indispensable (pedidos, pagos y notificaciones); panel de administración avanzado, inventario y reportes pasan a una versión 2.
**Ventajas:**

  * Cumple la fecha con un producto utilizable.
  * Permite obtener retroalimentación real del cliente temprano.
  * Reduce el riesgo de errores por apuro.
**Desventajas:**

  * El cliente debe aceptar que algunas funciones llegan después.
  * Requiere una conversación honesta sobre expectativas.
**Impacto en el proyecto:** el alcance se ajusta a la capacidad real del equipo.
