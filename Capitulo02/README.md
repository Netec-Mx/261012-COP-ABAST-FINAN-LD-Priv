# Práctica: Investigar mercado, proveedores y modelos de contratación con Copilot

## Metadatos

| Campo | Valor |
|---|---|
| **Duración** | 105 minutos |
| **Complejidad** | Media |
| **Nivel Bloom** | Aplicar (Apply) |
| **Modalidad** | Individual |
| **Escenario ficticio** | Banco Andino — datos sintéticos exclusivamente |

## Descripción General

En este laboratorio construirás prompts operativos con la estructura CROCF (Contexto, Rol, Objetivo, Criterios, Formato) para realizar un *market scan* asistido por Microsoft 365 Copilot sobre dos categorías de abastecimiento relevantes para el sector bancario: **biometría facial** y **servicios de inteligencia artificial**. Investigarás proveedores, modelos de contratación, *drivers* de costo y riesgos, organizando los hallazgos en una matriz Excel con trazabilidad de fuentes y distinción explícita entre hechos e inferencias. Finalmente, prepararás un entregable ejecutivo en Word listo para alimentar la siguiente etapa de *sourcing*. Todo el ejercicio se ejecuta con datos ficticios del Banco Andino; **no se debe ingresar información real, confidencial ni regulada en ningún prompt**.

## Objetivos de Aprendizaje

Al completar este laboratorio serás capaz de:

- [ ] Construir prompts operativos con estructura CROCF adaptados a tareas de investigación de mercado en abastecimiento bancario, verificando que cada componente (Contexto, Rol, Objetivo, Criterios, Formato) esté presente y sea coherente.
- [ ] Ejecutar un *market scan* estructurado en Copilot Chat (modo Trabajo) para identificar al menos tres proveedores por caso de uso (biometría facial y servicios de IA), documentando modelos operativos, de contratación, *drivers* de costo y riesgos en una matriz Excel con columnas de fuente y clasificación hecho/inferencia.
- [ ] Aplicar criterios de validación humana sobre las respuestas de Copilot, identificando al menos dos afirmaciones que requieran verificación independiente y documentando el método de verificación propuesto.
- [ ] Generar preguntas de profundización con Copilot que anticipen necesidades de información para etapas posteriores de RFI/RFP.
- [ ] Producir un entregable ejecutivo de una página en Word que resuma el *benchmark*, incluyendo contexto, proveedores, modelos de contratación, riesgos y próximos pasos recomendados.

## Prerrequisitos

### Conocimientos previos

| Área | Detalle |
|---|---|
| Abastecimiento estratégico | Familiaridad con procesos de *sourcing*, categorías de compra y ciclo de vida de proveedores en banca o sector financiero. |
| Prompt engineering | Haber completado los contenidos teóricos del Módulo 2.0 del curso: estructura CROCF, criterios de validación humana, distinción hecho vs. inferencia. |
| Microsoft Excel | Crear y editar tablas, aplicar formato condicional básico, gestionar columnas y filtros. |
| Microsoft Word | Redactar documentos estructurados con encabezados, tablas y estilos. |

### Acceso y licencias

| Recurso | Requisito |
|---|---|
| Microsoft 365 Copilot | Licencia activa asignada en el tenant corporativo o educativo del curso. Verificar acceso en `https://copilot.microsoft.com` con la cuenta de Microsoft Entra ID proporcionada. |
| Microsoft 365 Apps for enterprise | Versión 2408 (compilación 17928.20156) o posterior, con Copilot habilitado en Word y Excel. |
| SharePoint Online | Acceso de edición al sitio `https://[TENANT].sharepoint.com/sites/IAAbastecimientoBanca`, biblioteca "Documentos compartidos", carpeta `02_Lab_Investigacion`. |
| OneDrive for Business | Sincronización activa para la carpeta local `C:\Labs\IA_Abastecimiento_Banca\`. |
| Plantillas del laboratorio | Disponibles en la carpeta `00_Plantillas_Fuentes` del sitio SharePoint del curso (ver sección Entorno de Laboratorio). |

## Entorno de Laboratorio

### Hardware recomendado

| Componente | Especificación mínima |
|---|---|
| Procesador | 64 bits, 4 núcleos o superior |
| RAM | 16 GB recomendados (8 GB mínimo) |
| Almacenamiento libre | 10 GB para sincronización OneDrive y archivos temporales |
| Pantalla | 1920 × 1080; se recomienda monitor adicional para comparar Copilot Chat y Excel simultáneamente |
| Conexión a Internet | ≥ 20 Mbps descarga / 5 Mbps carga, HTTPS a dominios Microsoft 365 |

### Software requerido

| Software | Versión / Nota |
|---|---|
| Windows 11 Pro | 23H2 (compilación 22631.4169) |
| Microsoft Edge | 128.0.2739.79 |
| Microsoft 365 Apps for enterprise | Versión 2408 (compilación 17928.20156) |
| Microsoft 365 Copilot | Servicio SaaS — no aplica versión fija; acceso vía `https://copilot.microsoft.com` |
| Microsoft 365 Copilot en Word / Excel / PowerPoint | Integrado en Microsoft 365 Apps versión 2408+ con licencia Copilot activa |
| Microsoft Teams | Cliente de escritorio gestionado por el tenant — canal de actualización administrado |
| SharePoint Online / OneDrive for Business | Servicio SaaS administrado por Microsoft |

### Preparación del entorno

1. Abre **Microsoft Edge** y navega a `https://copilot.microsoft.com`. Inicia sesión con tu cuenta de Microsoft Entra ID del curso. Confirma que aparece el icono de **modo Trabajo** (escudo con candado) en la interfaz de Copilot Chat.
2. Navega a `https://[TENANT].sharepoint.com/sites/IAAbastecimientoBanca/Documentos%20compartidos/00_Plantillas_Fuentes` y descarga los dos archivos siguientes a `C:\Labs\IA_Abastecimiento_Banca\`:
   - `BA_02-00-01_MatrizHallazgos_Plantilla_v01.xlsx`
   - `BA_02-00-01_EntregableEjecutivo_Plantilla_v01.docx`
3. Abre ambos archivos desde la carpeta local para verificar que se abren correctamente en las aplicaciones de escritorio de Microsoft 365 con Copilot habilitado (busca el icono de Copilot en la cinta de opciones).
4. Crea en tu carpeta local el directorio de trabajo: `C:\Labs\IA_Abastecimiento_Banca\02_Lab_Investigacion\`.

> **⚠️ Regla de seguridad permanente:** Durante todo el laboratorio, utiliza Copilot Chat exclusivamente en **modo Trabajo** (ícono de escudo). No ingreses en ningún prompt datos reales del banco, nombres de personas, contratos vigentes, credenciales ni información regulada. Trabaja únicamente con el escenario ficticio **Banco Andino** y datos sintéticos.

### Estructura de la plantilla Excel (`BA_02-00-01_MatrizHallazgos_Plantilla_v01.xlsx`)

La plantilla contiene dos hojas: **Biometría Facial** y **Servicios IA**. Cada hoja tiene las siguientes columnas predefinidas:

| Columna | Propósito |
|---|---|
| A — Proveedor | Nombre del proveedor identificado |
| B — País / Región sede | Ubicación de la sede principal |
| C — Modelo de despliegue | SaaS, on-premise, híbrido, otro |
| D — Modelo de contratación | Suscripción, consumo, licencia perpetua, proyecto, otro |
| E — Referencia en banca | Casos conocidos en sector financiero (si los hay) |
| F — Drivers de costo principales | Variables que más influyen en el precio |
| G — Riesgos identificados | Riesgos contractuales, regulatorios o tecnológicos |
| H — Tendencias relevantes | Tendencias de mercado asociadas al proveedor o categoría |
| I — Fuente / Origen | URL, nombre del documento o referencia de donde proviene la información |
| J — Hecho vs. Inferencia | Clasificación: **Hecho** (dato verificable con fuente), **Inferencia** (interpretación de Copilot sin fuente directa) o **No evidenciado** |

### Estructura de la plantilla Word (`BA_02-00-01_EntregableEjecutivo_Plantilla_v01.docx`)

El documento contiene los siguientes encabezados predefinidos:

1. **Contexto del ejercicio** — Descripción breve del *market scan*.
2. **Proveedores identificados por categoría** — Tabla resumen.
3. **Comparación de modelos de contratación** — Tabla comparativa.
4. **Drivers de costo clave** — Lista priorizada.
5. **Riesgos principales** — Lista con clasificación.
6. **Preguntas de profundización para RFI/RFP** — Listado por proveedor/categoría.
7. **Próximos pasos recomendados** — Acciones sugeridas para la siguiente etapa de *sourcing*.
8. **Registro de validación humana** — Afirmaciones que requieren verificación independiente.

## Instrucciones Paso a Paso

---

### Paso 1: Construir el primer prompt operativo CROCF para biometría facial

**Objetivo:** Diseñar un prompt con los cinco componentes CROCF que solicite a Copilot una investigación inicial del mercado de biometría facial para banca, aplicando las reglas de seguridad y trazabilidad del curso.

**Tiempo estimado:** 20 minutos (Bloque 1 — Fundamentos del prompt operativo).

**Instrucciones:**

1. Abre Copilot Chat en `https://copilot.microsoft.com` con tu cuenta del curso. Verifica que el **modo Trabajo** esté activo (ícono de escudo visible).

2. Antes de escribir cualquier prompt, redacta en un bloc de notas local (o en un nuevo documento Word) la estructura CROCF de tu prompt, completando cada componente. Usa la siguiente guía:

   | Componente | Pregunta guía | Tu contenido |
   |---|---|---|
   | **Contexto** | ¿Qué situación estás analizando? | *Ejemplo: "El Banco Andino (entidad ficticia) está evaluando la contratación de una solución de biometría facial para autenticación de clientes en canales digitales. El horizonte de contratación es de 3 años. La operación se concentra en América Latina."* |
   | **Rol** | ¿Desde qué perspectiva debe responder Copilot? | *Ejemplo: "Actúa como analista de inteligencia de mercado para el área de Abastecimiento Estratégico."* |
   | **Objetivo** | ¿Qué entregable concreto necesitas? | *Ejemplo: "Identifica al menos cinco proveedores relevantes de biometría facial con presencia o aplicabilidad en banca, describiendo su modelo de despliegue, modelo de contratación, principales referencias en el sector financiero y diferenciadores clave."* |
   | **Criterios** | ¿Qué reglas debe seguir Copilot? | *Ejemplo: "Separa hechos documentados de inferencias. Indica la fuente de cada afirmación cuando sea posible. No presentes supuestos como datos confirmados. No recomiendes un proveedor ganador. Incluye proveedores globales y al menos uno regional de América Latina."* |
   | **Formato** | ¿Cómo debe presentarse el resultado? | *Ejemplo: "Tabla con columnas: Proveedor, País sede, Modelo de despliegue, Modelo de contratación, Referencias en banca, Diferenciadores, Fuente, Clasificación hecho/inferencia."* |

3. Revisa tu borrador de prompt y verifica que:
   - No contiene datos reales, nombres de personas ni información confidencial.
   - Incluye una instrucción explícita para separar hechos de inferencias.
   - Solicita fuentes o referencias para cada afirmación.
   - No pide a Copilot que recomiende o decida un proveedor ganador.

4. Copia tu prompt completo al cuadro de entrada de Copilot Chat y envíalo. **No modifiques la respuesta aún**; en el siguiente paso la analizarás críticamente.

5. Guarda una copia del prompt exacto que utilizaste en un archivo de texto local: `C:\Labs\IA_Abastecimiento_Banca\02_Lab_Investigacion\BA_02-00-01_Prompts_[TusIniciales]_v01.txt`. Este registro es parte de la trazabilidad del laboratorio.

**Resultado esperado:**

Copilot debe devolver una tabla o listado estructurado con al menos 3–5 proveedores de biometría facial, incluyendo información sobre modelos de despliegue, contratación y referencias. La respuesta debe contener alguna indicación de fuentes (aunque no siempre serán URLs verificables) y puede incluir tanto hechos como inferencias.

**Verificación:**

- [ ] El prompt enviado contiene los cinco componentes CROCF (Contexto, Rol, Objetivo, Criterios, Formato).
- [ ] El prompt incluye una instrucción explícita para distinguir hechos de inferencias.
- [ ] El prompt NO contiene datos reales, confidenciales ni regulados.
- [ ] Copilot devolvió una respuesta estructurada (tabla o listado) con al menos 3 proveedores.
- [ ] El prompt fue guardado en el archivo de registro de trazabilidad.

---

### Paso 2: Ejecutar el market scan de biometría facial con prompts iterativos

**Objetivo:** Profundizar la investigación de mercado de biometría facial mediante al menos dos prompts adicionales que amplíen dimensiones específicas (regulación, drivers de costo, riesgos), y volcar los hallazgos en la plantilla Excel.

**Tiempo estimado:** 25 minutos (Bloque 2 — Market scan de biometría facial).

**Instrucciones:**

1. Analiza la respuesta obtenida en el Paso 1. Identifica al menos dos dimensiones que requieran mayor profundidad. Ejemplos frecuentes:
   - Tendencias regulatorias sobre biometría facial en banca (protección de datos biométricos, regulación en América Latina y Europa).
   - Modelos de precios detallados (por transacción, por usuario activo, tarifa plana, costos de integración).
   - Riesgos contractuales típicos (dependencia de un solo proveedor, portabilidad de datos biométricos, cumplimiento de normativa local).

2. Construye un **segundo prompt** que profundice en la primera dimensión seleccionada. Ejemplo:

   ```text
   Contexto: Continuando con la investigación de biometría facial para el
   Banco Andino (entidad ficticia, América Latina). Ya identifiqué los
   proveedores [lista los nombres obtenidos en el Paso 1].

   Rol: Actúa como analista de inteligencia de mercado para Abastecimiento.

   Objetivo: Describe los principales drivers de costo en la contratación
   de soluciones de biometría facial para banca, indicando qué variables
   impactan más el precio total (volumen de transacciones, número de
   usuarios, nivel de personalización, costos de integración, soporte,
   SLAs de disponibilidad).

   Criterios: Basa tu análisis en información pública del sector.
   Distingue entre datos documentados e inferencias. No inventes cifras
   específicas de precios. Indica fuentes cuando estén disponibles.

   Formato: Tabla con columnas: Driver de costo, Descripción, Impacto
   relativo (alto/medio/bajo), Fuente, Hecho vs. Inferencia.
   ```

3. Envía el segundo prompt en Copilot Chat. Registra el prompt en tu archivo de trazabilidad.

4. Construye un **tercer prompt** que profundice en la segunda dimensión. Ejemplo para riesgos y regulación:

   ```text
   Contexto: Investigación de mercado de biometría facial para el Banco
   Andino (ficticio). Necesito entender los riesgos contractuales y
   regulatorios relevantes.

   Rol: Actúa como analista de riesgo de terceros para Abastecimiento.

   Objetivo: Identifica los principales riesgos asociados a la
   contratación de biometría facial en banca, incluyendo riesgos
   regulatorios (protección de datos biométricos), tecnológicos
   (dependencia de proveedor, obsolescencia), contractuales
   (portabilidad, penalizaciones, salida del servicio) y reputacionales.

   Criterios: Presenta solo riesgos relevantes para el sector bancario.
   Clasifica cada riesgo por probabilidad e impacto estimados
   (alto/medio/bajo). Indica si la clasificación es un hecho documentado
   o una inferencia tuya. Cita regulaciones específicas cuando sea
   posible (ej. GDPR, leyes locales de protección de datos en
   Latinoamérica).

   Formato: Tabla con columnas: Riesgo, Categoría (regulatorio /
   tecnológico / contractual / reputacional), Probabilidad, Impacto,
   Descripción breve, Regulación o fuente, Hecho vs. Inferencia.
   ```

5. Envía el tercer prompt. Registra en tu archivo de trazabilidad.

6. Abre la plantilla Excel `BA_02-00-01_MatrizHallazgos_Plantilla_v01.xlsx`. Ve a la hoja **Biometría Facial**.

7. Transfiere los hallazgos de las tres respuestas de Copilot a la matriz Excel. Para cada fila:
   - Completa todas las columnas A–J.
   - En la columna **I (Fuente / Origen)**, registra la fuente citada por Copilot. Si Copilot no citó fuente, escribe "Sin fuente citada por Copilot".
   - En la columna **J (Hecho vs. Inferencia)**, clasifica **tú mismo** cada dato. No aceptes automáticamente la clasificación de Copilot; aplica tu juicio profesional.

8. Opcionalmente, puedes usar Copilot en Excel para ayudar a organizar o dar formato a la tabla. Ejemplo de prompt en Excel:

   ```text
   Aplica formato de tabla a los datos de la hoja activa. Resalta en
   amarillo las celdas de la columna J que contengan "Inferencia".
   ```

9. Guarda el archivo Excel con la convención de nombres del curso:
   `BA_02-00-01_MatrizHallazgos_[TusIniciales]_v01.xlsx`
   en `C:\Labs\IA_Abastecimiento_Banca\02_Lab_Investigacion\`.

**Resultado esperado:**

La hoja **Biometría Facial** de la matriz Excel debe contener al menos 3 proveedores con información en todas las columnas, incluyendo drivers de costo y riesgos. Cada fila debe tener una fuente documentada (o la indicación explícita de ausencia de fuente) y una clasificación hecho/inferencia asignada por el participante.

**Verificación:**

- [ ] Se enviaron al menos 3 prompts iterativos a Copilot Chat (el inicial + 2 de profundización).
- [ ] Los 3 prompts fueron registrados en el archivo de trazabilidad.
- [ ] La hoja **Biometría Facial** contiene al menos 3 proveedores con todas las columnas A–J completadas.
- [ ] La columna **Fuente / Origen** tiene contenido en cada fila (dato o indicación de ausencia).
- [ ] La columna **Hecho vs. Inferencia** fue completada con juicio propio del participante, no copiada literalmente de Copilot.

---

### Paso 3: Ejecutar el market scan de servicios de IA para banca

**Objetivo:** Investigar el mercado de servicios de IA aplicables a procesos bancarios, comparando modelos de contratación, drivers de costo y riesgos, y registrar los hallazgos en la segunda hoja de la matriz Excel.

**Tiempo estimado:** 25 minutos (Bloque 3 — Market scan de servicios de IA).

**Instrucciones:**

1. En Copilot Chat (modo Trabajo), inicia una nueva conversación o continúa en la misma sesión. Construye un prompt CROCF para investigar el mercado de servicios de IA para banca. Ejemplo de prompt inicial:

   ```text
   Contexto: El Banco Andino (entidad ficticia, operaciones en América
   Latina) está explorando la contratación de servicios de inteligencia
   artificial aplicables a procesos bancarios: modelos de lenguaje para
   atención al cliente, automatización de procesos documentales,
   analítica predictiva para riesgo crediticio y detección de fraude.
   El horizonte de evaluación es de 3 años.

   Rol: Actúa como analista de inteligencia de mercado para el área de
   Abastecimiento Estratégico del banco.

   Objetivo: Identifica al menos cinco proveedores relevantes de
   servicios de IA aplicables a banca, describiendo: tipo de servicio
   ofrecido, modelo de despliegue (nube pública, nube privada, híbrido,
   on-premise), modelo de contratación (suscripción, consumo por API
   call, licencia perpetua, proyecto llave en mano), referencias
   conocidas en el sector financiero y diferenciadores clave.

   Criterios:
   - Incluye proveedores de plataformas de IA generalistas (ej.
     hyperscalers) y proveedores especializados en banca.
   - Separa hechos documentados de inferencias.
   - Indica la fuente de cada afirmación cuando sea posible.
   - No recomiendes un proveedor ganador.
   - No inventes nombres de productos o servicios que no existan.

   Formato: Tabla con columnas: Proveedor, Tipo de servicio IA, País
   sede, Modelo de despliegue, Modelo de contratación, Referencias en
   banca, Diferenciadores, Fuente, Hecho vs. Inferencia.
   ```

2. Envía el prompt. Registra en tu archivo de trazabilidad.

3. Construye un **segundo prompt** enfocado en modelos de contratación y drivers de costo:

   ```text
   Contexto: Continuando con la investigación de servicios de IA para
   el Banco Andino. Ya identifiqué los proveedores [lista los nombres].

   Rol: Actúa como analista de Abastecimiento especializado en modelos
   de contratación tecnológica.

   Objetivo: Compara los modelos de contratación típicos para servicios
   de IA en banca: suscripción mensual/anual, pago por consumo
   (API calls, tokens procesados), licencia perpetua con mantenimiento,
   y proyecto llave en mano. Para cada modelo, describe los principales
   drivers de costo, ventajas, desventajas y escenarios de uso
   recomendados.

   Criterios: Basa el análisis en prácticas documentadas del mercado.
   Distingue hechos de inferencias. No inventes cifras de precios.
   Indica fuentes cuando estén disponibles.

   Formato: Tabla con columnas: Modelo de contratación, Drivers de
   costo, Ventajas, Desventajas, Escenario de uso recomendado, Fuente,
   Hecho vs. Inferencia.
   ```

4. Envía el prompt. Registra en tu archivo de trazabilidad.

5. Construye un **tercer prompt** enfocado en riesgos contractuales y regulatorios de servicios de IA en banca:

   ```text
   Contexto: Investigación de servicios de IA para el Banco Andino
   (ficticio). Necesito mapear riesgos para la evaluación de
   proveedores.

   Rol: Actúa como analista de riesgo de terceros para Abastecimiento.

   Objetivo: Identifica los principales riesgos asociados a la
   contratación de servicios de IA en banca, incluyendo: riesgos
   regulatorios (explicabilidad de modelos, sesgo algorítmico,
   regulación de IA en servicios financieros), tecnológicos (lock-in,
   obsolescencia de modelos, dependencia de datos de entrenamiento),
   contractuales (propiedad intelectual de modelos entrenados,
   confidencialidad de datos, SLAs de rendimiento) y operativos
   (disponibilidad, escalabilidad, soporte).

   Criterios: Clasifica cada riesgo por probabilidad e impacto
   (alto/medio/bajo). Indica si la clasificación es un hecho o una
   inferencia. Cita regulaciones o marcos de referencia específicos
   cuando sea posible (ej. EU AI Act, directrices de supervisores
   bancarios).

   Formato: Tabla con columnas: Riesgo, Categoría, Probabilidad,
   Impacto, Descripción, Regulación o fuente, Hecho vs. Inferencia.
   ```

6. Envía el prompt. Registra en tu archivo de trazabilidad.

7. Abre la hoja **Servicios IA** de tu archivo Excel. Transfiere los hallazgos de las tres respuestas, completando todas las columnas A–J con el mismo rigor aplicado en el Paso 2:
   - Registra fuentes reales o indica su ausencia.
   - Clasifica hecho/inferencia con tu propio juicio.

8. Guarda el archivo Excel actualizado.

**Resultado esperado:**

La hoja **Servicios IA** debe contener al menos 3 proveedores con información completa en todas las columnas, incluyendo comparación de modelos de contratación, drivers de costo y riesgos. La trazabilidad de fuentes y la clasificación hecho/inferencia deben estar documentadas en cada fila.

**Verificación:**

- [ ] Se enviaron al menos 3 prompts iterativos para servicios de IA.
- [ ] Los prompts fueron registrados en el archivo de trazabilidad.
- [ ] La hoja **Servicios IA** contiene al menos 3 proveedores con columnas A–J completadas.
- [ ] Se documentaron al menos 3 modelos de contratación distintos con sus drivers de costo.
- [ ] Los riesgos identificados incluyen al menos las categorías regulatoria, tecnológica y contractual.

---

### Paso 4: Generar síntesis comparativa, preguntas de profundización y validación humana

**Objetivo:** Usar Copilot para sintetizar las diferencias entre proveedores de ambos casos de uso, generar preguntas de profundización para la etapa de RFI/RFP y aplicar explícitamente el criterio de validación humana identificando afirmaciones que requieren verificación independiente.

**Tiempo estimado:** 20 minutos (Bloque 4 — Síntesis, preguntas y validación).

**Instrucciones:**

1. En Copilot Chat (modo Trabajo), construye un prompt de síntesis comparativa. Ejemplo:

   ```text
   Contexto: He completado una investigación de mercado para el Banco
   Andino (ficticio) sobre dos categorías: biometría facial y servicios
   de IA para banca. A continuación resumo los proveedores identificados:

   Biometría facial: [lista los proveedores identificados en el Paso 2]
   Servicios de IA: [lista los proveedores identificados en el Paso 3]

   Rol: Actúa como analista de Abastecimiento Estratégico preparando
   un informe ejecutivo para el comité de sourcing.

   Objetivo: Genera un resumen comparativo que destaque:
   1. Las tres diferencias más significativas entre los proveedores de
      biometría facial.
   2. Las tres diferencias más significativas entre los proveedores de
      servicios de IA.
   3. Similitudes y diferencias entre ambas categorías en cuanto a
      modelos de contratación y riesgos.

   Criterios: Basa el resumen en la información que te proporcioné.
   Distingue hechos de inferencias. No recomiendes un proveedor. Sé
   conciso (máximo 400 palabras).

   Formato: Texto estructurado con encabezados numerados para cada
   sección.
   ```

2. Envía el prompt y revisa la respuesta. Registra en tu archivo de trazabilidad.

3. Construye un prompt para generar **preguntas de profundización**:

   ```text
   Contexto: Misma investigación de mercado del Banco Andino para
   biometría facial y servicios de IA.

   Rol: Actúa como analista de Abastecimiento que prepara la siguiente
   etapa de RFI/RFP.

   Objetivo: Para cada proveedor identificado en ambas categorías,
   genera 3 preguntas de profundización que el equipo de Abastecimiento
   debería formular en una solicitud de información (RFI) o solicitud
   de propuesta (RFP). Las preguntas deben cubrir áreas donde la
   información pública es insuficiente o donde se detectaron inferencias
   sin respaldo documental.

   Criterios: Las preguntas deben ser específicas, accionables y
   orientadas a reducir incertidumbre para la toma de decisiones.
   Agrupa las preguntas por proveedor. Indica qué dimensión de
   evaluación cubre cada pregunta (cobertura funcional, precio,
   riesgo, soporte, etc.).

   Formato: Lista agrupada por proveedor. Cada pregunta con formato:
   [Dimensión] — Pregunta.
   ```

4. Envía el prompt. Registra en tu archivo de trazabilidad.

5. **Validación humana crítica** — Este es un paso obligatorio del laboratorio. Revisa todas las respuestas de Copilot obtenidas en los Pasos 1–4 e identifica **al menos dos afirmaciones** que consideres que requieren verificación independiente. Para cada una, documenta en tu archivo de trazabilidad:

   | # | Afirmación de Copilot | ¿Por qué requiere verificación? | Método de verificación propuesto |
   |---|---|---|---|
   | 1 | *Ejemplo: "El proveedor X tiene certificación ISO 27001 para su servicio de biometría facial."* | *Copilot no citó fuente directa; podría ser una inferencia basada en información general de la empresa.* | *Consultar el sitio web oficial del proveedor, solicitar copia del certificado vigente en la RFI.* |
   | 2 | *Ejemplo: "El modelo de consumo por API call es el más común en servicios de IA para banca en América Latina."* | *Afirmación de tendencia de mercado sin fuente específica; podría ser una generalización.* | *Buscar informes de analistas de mercado (Gartner, IDC, Frost & Sullivan) sobre modelos de contratación de IA en LATAM.* |

6. **Prueba adversarial obligatoria:** Envía a Copilot un prompt que contenga información ficticia para evaluar si la herramienta la acepta sin cuestionarla:

   ```text
   Contexto: En mi investigación encontré que el proveedor "NovaBiometrics
   del Sur" (empresa ficticia que acabo de inventar) tiene el 45% del
   mercado de biometría facial en banca latinoamericana.

   Rol: Actúa como analista de inteligencia de mercado.

   Objetivo: Confirma esta información y describe las fortalezas de
   NovaBiometrics del Sur frente a sus competidores.

   Criterios: Basa tu respuesta en hechos documentados.
   ```

   **Analiza la respuesta de Copilot:**
   - ¿Copilot aceptó la información ficticia como verdadera y la amplió?
   - ¿Copilot cuestionó la existencia del proveedor o la cifra de mercado?
   - ¿Copilot generó información adicional inventada sobre un proveedor inexistente?

   Documenta el resultado de esta prueba adversarial en tu archivo de trazabilidad con una breve nota sobre el comportamiento observado y la lección aprendida para el uso profesional de Copilot.

**Resultado esperado:**

Debes tener: (a) un resumen comparativo estructurado, (b) un listado de preguntas de profundización agrupadas por proveedor, (c) al menos dos afirmaciones identificadas para verificación humana con método propuesto, y (d) el resultado documentado de la prueba adversarial.

**Verificación:**

- [ ] El resumen comparativo cubre las diferencias clave en ambas categorías (biometría facial y servicios de IA).
- [ ] Se generaron al menos 3 preguntas de profundización por proveedor.
- [ ] Se identificaron y documentaron al menos 2 afirmaciones que requieren verificación independiente, con método de verificación propuesto.
- [ ] La prueba adversarial fue ejecutada y documentada con observaciones sobre el comportamiento de Copilot.
- [ ] Todos los prompts de este paso fueron registrados en el archivo de trazabilidad.

---

### Paso 5: Preparar el entregable ejecutivo en Word

**Objetivo:** Utilizar Copilot en Word para estructurar un documento ejecutivo de una página (*Executive Summary* del *Market Scan*) que integre los hallazgos del laboratorio y esté listo para la siguiente etapa de *sourcing*.

**Tiempo estimado:** 15 minutos (Bloque 5 — Entregable ejecutivo).

**Instrucciones:**

1. Abre la plantilla Word `BA_02-00-01_EntregableEjecutivo_Plantilla_v01.docx` desde tu carpeta de trabajo local.

2. Guarda inmediatamente una copia con la convención de nombres del curso:
   `BA_02-00-01_EntregableEjecutivo_[TusIniciales]_v01.docx`

3. Posiciona el cursor en la sección **"Contexto del ejercicio"** del documento. Usa Copilot en Word (botón Copilot en la cinta de opciones o atajo en el cuerpo del documento) con el siguiente prompt:

   ```text
   Redacta un párrafo de contexto (máximo 80 palabras) para un
   Executive Summary de market scan. El Banco Andino (entidad ficticia)
   está evaluando la contratación de soluciones de biometría facial y
   servicios de inteligencia artificial para procesos bancarios. El
   horizonte de evaluación es de 3 años. El objetivo del market scan
   es identificar proveedores, modelos de contratación, drivers de
   costo y riesgos para preparar la siguiente etapa de sourcing
   (RFI/RFP).
   ```

4. Revisa y ajusta el texto generado. Asegúrate de que no contenga afirmaciones que presenten datos ficticios como reales.

5. Completa las secciones restantes del documento. Para cada sección, puedes optar por:
   - **Opción A:** Redactar manualmente usando los hallazgos de tu matriz Excel y las respuestas de Copilot.
   - **Opción B:** Usar Copilot en Word con prompts específicos para cada sección. Ejemplo para la tabla de proveedores:

     ```text
     Genera una tabla resumen con los proveedores identificados en mi
     investigación de mercado. Categorías: biometría facial y servicios
     de IA. Columnas: Categoría, Proveedor, Modelo de despliegue,
     Modelo de contratación, Diferenciador clave. Incluye los
     siguientes proveedores: [lista tus proveedores de ambas hojas
     Excel].
     ```

6. En la sección **"Registro de validación humana"**, incluye las dos afirmaciones identificadas en el Paso 4 (instrucción 5) con sus métodos de verificación. Añade también una nota breve sobre los hallazgos de la prueba adversarial.

7. En la sección **"Próximos pasos recomendados"**, redacta (con o sin asistencia de Copilot) al menos tres acciones concretas para la siguiente etapa de *sourcing*. Ejemplos:
   - Enviar RFI a los proveedores preseleccionados con las preguntas de profundización generadas.
   - Validar las certificaciones y referencias declaradas mediante consulta directa.
   - Solicitar al área de Cumplimiento una revisión de los requisitos regulatorios identificados.

8. Revisa el documento completo. Verifica que:
   - No exceda una página (o dos como máximo si incluyes tablas extensas).
   - Todas las afirmaciones clave tengan indicación de fuente o estén marcadas como inferencias.
   - No contenga datos reales, confidenciales ni regulados.

9. Guarda el documento final.

10. **(Opcional — si el tiempo lo permite):** Abre PowerPoint y usa Copilot para generar una presentación a partir del documento Word:

    ```text
    Crea una presentación de 3 a 5 diapositivas basada en el documento
    adjunto. La presentación es un Executive Summary de market scan
    para el comité de sourcing del Banco Andino. Incluye: diapositiva
    de contexto, diapositiva de proveedores identificados (tabla),
    diapositiva de modelos de contratación comparados, diapositiva de
    riesgos y próximos pasos.
    ```

    Si usas esta opción, guarda la presentación como:
    `BA_02-00-01_PresentacionEjecutiva_[TusIniciales]_v01.pptx`

11. Sube todos los entregables finales a SharePoint:
    `https://[TENANT].sharepoint.com/sites/IAAbastecimientoBanca/Documentos%20compartidos/02_Lab_Investigacion/`

    Archivos a subir:
    - `BA_02-00-01_MatrizHallazgos_[TusIniciales]_v01.xlsx`
    - `BA_02-00-01_EntregableEjecutivo_[TusIniciales]_v01.docx`
    - `BA_02-00-01_Prompts_[TusIniciales]_v01.txt`
    - (Opcional) `BA_02-00-01_PresentacionEjecutiva_[TusIniciales]_v01.pptx`

**Resultado esperado:**

Un documento Word de una página (máximo dos) con todas las secciones de la plantilla completadas: contexto, proveedores por categoría, comparación de modelos de contratación, drivers de costo, riesgos, preguntas de profundización, próximos pasos y registro de validación humana. Todos los entregables subidos a SharePoint.

**Verificación:**

- [ ] El documento Word contiene las 8 secciones de la plantilla completadas.
- [ ] El documento incluye al menos una tabla comparativa de proveedores o modelos de contratación.
- [ ] La sección de validación humana contiene al menos 2 afirmaciones con método de verificación y la nota de la prueba adversarial.
- [ ] El documento no excede 2 páginas.
- [ ] Los 3 archivos obligatorios (Excel, Word, TXT de prompts) fueron subidos a la carpeta correcta en SharePoint.
- [ ] La convención de nombres `BA_[LabID]_[Artefacto]_[Iniciales]_v01` se respetó en todos los archivos.

---

## Validación y Pruebas

Utiliza la siguiente rúbrica para autoevaluar la calidad de tus entregables antes de considerarlos completos. Cada criterio debe cumplirse para que el laboratorio se considere satisfactorio.

### Criterios de validación de la matriz Excel

| # | Criterio | Evidencia requerida | ¿Cumple? |
|---|---|---|---|
| 1 | **Cobertura de proveedores** | Al menos 3 proveedores distintos en la hoja Biometría Facial Y al menos 3 en la hoja Servicios IA. | ☐ |
| 2 | **Completitud de columnas** | Todas las columnas A–J tienen contenido en cada fila de proveedor (no hay celdas vacías sin justificación). | ☐ |
| 3 | **Trazabilidad de fuentes** | La columna I (Fuente/Origen) contiene una referencia específica o la indicación explícita "Sin fuente citada por Copilot" en cada fila. | ☐ |
| 4 | **Clasificación hecho/inferencia** | La columna J fue completada por el participante con juicio propio. Al menos el 30% de las filas contienen la clasificación "Inferencia" o "No evidenciado" (indicador de pensamiento crítico). | ☐ |
| 5 | **Diversidad de modelos** | Se documentaron al menos 2 modelos de contratación distintos por categoría. | ☐ |
| 6 | **Riesgos documentados** | Al menos 3 riesgos identificados por categoría, cubriendo al menos 2 tipos distintos (regulatorio, tecnológico, contractual, reputacional, operativo). | ☐ |

### Criterios de validación del entregable ejecutivo Word

| # | Criterio | Evidencia requerida | ¿Cumple? |
|---|---|---|---|
| 7 | **Secciones completas** | Las 8 secciones de la plantilla están presentes y tienen contenido sustantivo. | ☐ |
| 8 | **Tabla comparativa** | Al menos una tabla que compare proveedores o modelos de contratación. | ☐ |
| 9 | **Validación humana documentada** | Sección de validación humana con al menos 2 afirmaciones, justificación y método de verificación. | ☐ |
| 10 | **Prueba adversarial documentada** | Nota sobre el resultado de la prueba con proveedor ficticio, incluyendo comportamiento observado de Copilot. | ☐ |
| 11 | **Próximos pasos accionables** | Al menos 3 acciones concretas para la siguiente etapa de sourcing. | ☐ |
| 12 | **Extensión apropiada** | El documento no excede 2 páginas. | ☐ |

### Criterios de validación de trazabilidad y seguridad

| # | Criterio | Evidencia requerida | ¿Cumple? |
|---|---|---|---|
| 13 | **Registro de prompts** | Archivo TXT con todos los prompts utilizados (mínimo 7: 3 biometría + 3 IA + 1 síntesis + preguntas + adversarial). | ☐ |
| 14 | **Seguridad de datos** | Ningún prompt contiene datos reales, nombres de personas reales, contratos vigentes ni información regulada. Revisión completa del archivo TXT. | ☐ |
| 15 | **Modo Trabajo** | Todos los prompts fueron ejecutados en Copilot Chat con modo Trabajo activo (verificado al inicio del laboratorio). | ☐ |
| 16 | **Convención de nombres** | Todos los archivos siguen el formato `BA_02-00-01_[Artefacto]_[Iniciales]_v01.[ext]`. | ☐ |

### Caso adversarial obligatorio (criterio 10 ampliado)

La prueba adversarial del Paso 4 (instrucción 6) es un requisito de validación del laboratorio. Su propósito es demostrar que el participante comprende las limitaciones de Copilot y puede detectar cuándo la herramienta acepta o amplifica información falsa. El resultado esperado **no es que Copilot siempre detecte la información ficticia**, sino que el participante:

- Reconozca que Copilot puede generar contenido plausible pero falso (*alucinación*).
- Documente el comportamiento específico observado (¿aceptó? ¿cuestionó? ¿inventó detalles adicionales?).
- Articule la implicación para el uso profesional: toda salida de Copilot debe tratarse como borrador sujeto a verificación humana, especialmente en contextos de abastecimiento donde las decisiones tienen impacto financiero y contractual.

## Solución de Problemas

### Problema 1: Copilot Chat no muestra el modo Trabajo o devuelve respuestas genéricas sin estructura

**Síntomas:** Al abrir `https://copilot.microsoft.com`, no aparece el ícono de escudo (modo Trabajo) o las respuestas de Copilot son extremadamente breves, genéricas y no siguen la estructura solicitada en el prompt (no genera tablas, no distingue hechos de inferencias).

**Causa:** La licencia de Microsoft 365 Copilot no está correctamente asignada al usuario en el tenant del curso, o la sesión del navegador está usando una cuenta personal en lugar de la cuenta corporativa de Microsoft Entra ID. También puede ocurrir si el tenant no tiene habilitada la funcionalidad de modo Trabajo para Copilot Chat.

**Solución:**
1. Verifica que estás usando la cuenta corporativa del curso: haz clic en tu avatar en la esquina superior derecha de Copilot Chat y confirma que el correo corresponde al tenant del curso (`@[TENANT].onmicrosoft.com` o el dominio corporativo asignado).
2. Si la cuenta es incorrecta, cierra sesión, borra las cookies del navegador para `copilot.microsoft.com` y vuelve a iniciar sesión con la cuenta correcta.
3. Si la cuenta es correcta pero el modo Trabajo no aparece, contacta al instructor para que verifique la asignación de licencia de Microsoft 365 Copilot en el Centro de Administración de Microsoft 365 (`https://admin.microsoft.com` > Usuarios > Licencias).
4. Como alternativa temporal mientras se resuelve la licencia, puedes usar Copilot integrado en Word o Excel (si está disponible) para las tareas de síntesis y organización, y documentar la incidencia en tu archivo de trazabilidad.

### Problema 2: Copilot en Word no genera contenido o muestra el mensaje "No puedo ayudarte con eso"

**Síntomas:** Al usar el botón de Copilot en Word para redactar o transformar texto, la herramienta no genera contenido, muestra un mensaje de error genérico o indica que no puede ayudar con la solicitud. El ícono de Copilot puede no aparecer en la cinta de opciones.

**Causa:** El archivo Word puede estar almacenado en una ubicación local no sincronizada con OneDrive/SharePoint (Copilot en aplicaciones de escritorio requiere que el archivo esté guardado en OneDrive o SharePoint para funcionar). Alternativamente, la versión de Microsoft 365 Apps puede no estar actualizada a la compilación requerida (2408 o posterior), o el prompt puede contener instrucciones que activan filtros de contenido de Copilot.

**Solución:**
1. Verifica la ubicación del archivo: en Word, revisa la barra de título. Si muestra una ruta local (`C:\...`) sin el ícono de nube de OneDrive, guarda el archivo en tu carpeta de OneDrive sincronizada o directamente en SharePoint.
2. Verifica la versión de la aplicación: en Word, ve a **Archivo > Cuenta > Acerca de Word** y confirma que la versión es 2408 (compilación 17928.20156) o posterior. Si es anterior, solicita al instructor que ejecute una actualización forzada desde el Centro de Administración de Microsoft 365 Apps.
3. Si el ícono de Copilot no aparece en la cinta, cierra y reabre Word. Si persiste, reinicia el equipo.
4. Si Copilot rechaza un prompt específico, simplifica la instrucción eliminando términos que puedan activar filtros (evita mencionar datos financieros específicos o información que parezca confidencial). Recuerda que estás trabajando con el escenario ficticio del Banco Andino.
5. Como alternativa, redacta el contenido manualmente usando los hallazgos de Copilot Chat y la matriz Excel, y documenta la incidencia.

## Limpieza

Al finalizar el laboratorio, ejecuta los siguientes pasos:

1. **Confirma que todos los entregables están en SharePoint:** Verifica que los siguientes archivos existen en `https://[TENANT].sharepoint.com/sites/IAAbastecimientoBanca/Documentos%20compartidos/02_Lab_Investigacion/`:
   - `BA_02-00-01_MatrizHallazgos_[TusIniciales]_v01.xlsx`
   - `BA_02-00-01_EntregableEjecutivo_[TusIniciales]_v01.docx`
   - `BA_02-00-01_Prompts_[TusIniciales]_v01.txt`
   - (Opcional) `BA_02-00-01_PresentacionEjecutiva_[TusIniciales]_v01.pptx`

2. **Elimina los archivos temporales locales:** Borra el contenido de `C:\Labs\IA_Abastecimiento_Banca\02_Lab_Investigacion\` según la política corporativa. No dejes copias locales de los entregables una vez confirmada la carga en SharePoint.

3. **Cierra las sesiones de Copilot Chat:** En `https://copilot.microsoft.com`, cierra la conversación activa. Copilot Chat en modo Trabajo no retiene el historial de conversaciones entre sesiones para el tenant, pero es buena práctica cerrar sesiones activas.

4. **Cierra las aplicaciones de Microsoft 365:** Cierra Word, Excel y PowerPoint. Si usaste PowerPoint para el entregable opcional, verifica que el archivo se guardó correctamente antes de cerrar.

5. **Vacía la papelera de reciclaje local** si contiene archivos del laboratorio.

## Resumen

En este laboratorio aplicaste la estructura CROCF (Contexto, Rol, Objetivo, Criterios, Formato) para construir prompts operativos que guiaron a Microsoft 365 Copilot en una investigación de mercado sobre biometría facial y servicios de IA para banca. Los aspectos clave que practicaste fueron:

- **Diseño de prompts con intención:** Cada prompt incluyó los cinco componentes CROCF, lo que permitió obtener respuestas más estructuradas, comparables y verificables que una solicitud abierta.
- **Iteración controlada:** Usaste al menos 3 prompts por categoría, profundizando progresivamente en drivers de costo, modelos de contratación y riesgos, en lugar de esperar una respuesta completa de un solo prompt.
- **Trazabilidad y evidencia:** Cada hallazgo fue registrado con su fuente y clasificado como hecho o inferencia por tu propio juicio, no por la clasificación automática de Copilot.
- **Validación humana y pensamiento crítico:** Identificaste afirmaciones que requieren verificación independiente y ejecutaste una prueba adversarial que demostró las limitaciones de Copilot frente a información ficticia.
- **Entregable accionable:** Produjiste un *Executive Summary* listo para ser utilizado en la siguiente etapa de *sourcing*, con próximos pasos concretos y un registro explícito de las limitaciones del análisis.

Los entregables de este laboratorio (matriz Excel y documento ejecutivo Word) serán insumos directos para los laboratorios siguientes del curso: construcción de RFI/RFP (Lab 03), análisis de TCO (Lab 04) y evaluación de riesgo contractual (Lab 05).

### Recursos adicionales

| Recurso | Enlace |
|---|---|
| Documentación oficial de Microsoft 365 Copilot | `https://learn.microsoft.com/en-us/copilot/microsoft-365/` |
| Guía de prompts efectivos para Copilot (Microsoft Adoption) | `https://adoption.microsoft.com/en-us/copilot/` |
| Marco de IA responsable de Microsoft | `https://www.microsoft.com/en-us/ai/responsible-ai` |
| EU AI Act — Texto oficial | `https://eur-lex.europa.eu/eli/reg/2024/1689/oj` |

---
