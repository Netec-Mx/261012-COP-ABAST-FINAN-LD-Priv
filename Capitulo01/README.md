# Práctica: Mapear el proceso de Abastecimiento e identificar oportunidades de uso de Copilot

## Metadatos

| Campo | Valor |
|---|---|
| **Duración** | 90 minutos |
| **Complejidad** | Media |
| **Nivel Bloom** | Aplicar (Apply) |
| **Módulo** | 1.0 — Referentes y oportunidades de IA en Abastecimiento bancario |
| **Dependencias previas** | Ningún laboratorio anterior; es el primer laboratorio del curso |

## Descripción General

En este laboratorio los participantes utilizarán Microsoft 365 Copilot Chat para mapear el proceso de Abastecimiento Estratégico de "Banco Andino" e identificar oportunidades concretas de apoyo con IA en cada etapa. Se trabajará con tres casos de negocio con datos cuantitativos específicos —biometría facial, contratación de IA y Contact Center— construyendo prompts progresivos que extraigan variables, supuestos, información faltante y tareas asociadas. Los entregables —una Matriz de Mapeo y una Matriz de Oportunidades en Excel— servirán como insumos base para todos los laboratorios subsiguientes del curso.

## Objetivos de Aprendizaje

Al completar este laboratorio, serás capaz de:

- [ ] Construir un mapa estructurado del proceso de Abastecimiento Estratégico bancario con al menos 7 etapas clave documentadas en una matriz Excel verificable.
- [ ] Formular prompts efectivos en Microsoft 365 Copilot Chat que incluyan rol, objetivo, contexto, fuentes, criterios de salida y reglas de validación para extraer variables críticas, supuestos e información faltante de los tres casos de negocio.
- [ ] Identificar y documentar al menos 3 oportunidades específicas de uso de Copilot por caso de negocio, clasificadas por etapa del proceso, herramienta aplicable, tipo de apoyo y nivel de impacto.
- [ ] Validar críticamente las respuestas de Copilot aplicando criterio de Abastecimiento para distinguir salidas útiles de salidas incompletas, no sustentadas o que requieren verificación adicional.
- [ ] Conectar lecciones aprendidas de los referentes Deutsche Bank (IA agentic para riesgo de terceros) y Hellenic Bank (transformación de Procurement con GEP) con las oportunidades identificadas para el contexto bancario latinoamericano.

## Prerrequisitos

### Conocimientos requeridos

| Área | Nivel esperado |
|---|---|
| Procesos de Abastecimiento Estratégico / Compras corporativas | Mínimo 1 año de experiencia en entorno corporativo o bancario |
| Microsoft 365 Copilot o Copilot Chat | Familiaridad básica: haber ejecutado al menos una sesión previa de prompts |
| Microsoft Excel | Crear y editar tablas, aplicar filtros y formato condicional |
| Microsoft Word | Documentar hallazgos en formato estructurado |
| Referentes del módulo | Haber leído el material sobre Deutsche Bank (IA agentic, riesgo de terceros) y Hellenic Bank (transformación Procurement con GEP), distribuido por el instructor vía Teams al menos 24 horas antes |

### Accesos y licencias requeridos

| Recurso | Requisito |
|---|---|
| Cuenta Microsoft Entra ID | Activa en el tenant de capacitación, verificada por el instructor antes del inicio |
| Licencia Microsoft 365 Copilot | Add-on habilitado sobre Microsoft 365 Apps for Enterprise, o al mínimo Copilot Chat con protección de datos comerciales |
| Microsoft Teams | Canal del curso accesible para recepción de materiales y plantillas |
| SharePoint / OneDrive | Acceso de edición al sitio `https://[TENANT].sharepoint.com/sites/IAAbastecimientoBanca` y a la carpeta `01_Lab_MapaProceso` |

> **Nota para el instructor:** Reemplace `[TENANT]` por el nombre real del tenant antes de distribuir esta guía. Verifique que todos los participantes puedan acceder al sitio de SharePoint y crear archivos en la carpeta `01_Lab_MapaProceso`.

## Entorno de Laboratorio

### Hardware mínimo

| Componente | Especificación |
|---|---|
| Procesador | 64 bits, 4 núcleos o superior |
| RAM | 16 GB recomendados (mínimo 8 GB) |
| Almacenamiento libre | 10 GB para sincronización de OneDrive y archivos temporales |
| Pantalla | 1920 × 1080 mínimo; se recomienda monitor adicional |
| Conectividad | 20 Mbps descarga / 5 Mbps carga; acceso HTTPS a dominios de Microsoft 365 |

### Software requerido

| Software | Versión exacta | Fuente oficial |
|---|---|---|
| Windows 11 Pro | 23H2, compilación 22631.4169 | https://www.microsoft.com/es-es/windows/windows-11 |
| Microsoft 365 Apps for Enterprise | Versión 2408, compilación 17928.20156 | https://learn.microsoft.com/es-es/officeupdates/update-history-microsoft365-apps-by-date |
| Microsoft Edge | 128.0.2739.79 | https://www.microsoft.com/es-es/edge |
| Microsoft Teams | Cliente de escritorio administrado por el tenant (canal Current) | https://www.microsoft.com/es-es/microsoft-teams/download-app |
| Microsoft OneDrive for Business | 24.211.1027.0001 | https://www.microsoft.com/es-es/microsoft-365/onedrive/download |
| Microsoft 365 Copilot | Servicio SaaS (sin versión fija publicable) | https://learn.microsoft.com/es-es/copilot/microsoft-365/microsoft-365-copilot-overview |
| Microsoft 365 Copilot Chat | Servicio SaaS (sin versión fija publicable) | https://copilot.microsoft.com |

### Preparación del directorio local

Abra una ventana de PowerShell y ejecute:

```powershell
## Crear directorio local temporal para el laboratorio
New-Item -ItemType Directory -Path "C:\Labs\IA_Abastecimiento_Banca\01_Lab_MapaProceso" -Force
```

Verifique que la carpeta existe:

```powershell
Test-Path "C:\Labs\IA_Abastecimiento_Banca\01_Lab_MapaProceso"
## Resultado esperado: True
```

### Datos de los tres casos de negocio (referencia obligatoria)

Los siguientes datos sintéticos del escenario ficticio "Banco Andino" se utilizarán en todos los prompts del laboratorio. **No se requiere archivo externo**; los datos se incorporan directamente en los prompts.

#### Caso 1: Biometría Facial

| Variable | Valor |
|---|---|
| Clientes actuales | 30 millones |
| Clientes proyectados | 40 millones |
| Transacciones anuales | 1 billón (1 × 10¹²) |
| SLA requerido | 99,9999 % de disponibilidad |
| Proveedores en el mercado | 10 compañías identificadas |

#### Caso 2: Contratación de IA (Plataforma de Modelos de Lenguaje)

| Variable | Valor |
|---|---|
| Consumo proyectado | 70 a 100 billones de tokens/año |
| Horizonte contractual | 5 años |

#### Caso 3: Contact Center

| Variable | Valor |
|---|---|
| Volumen de llamadas | 300 millones de llamadas/año |
| Indexación de costos | IPC del 6 % anual |
| Referencia salarial | SMMLV de 23 (salarios mínimos mensuales legales vigentes como unidad de medida) |

## Instrucciones Paso a Paso

---

### Paso 1: Configurar el espacio de trabajo y verificar accesos (10 min)

**Objetivo:** Confirmar que todos los accesos, herramientas y materiales están disponibles antes de iniciar las actividades de mapeo.

**Instrucciones:**

1. Abra Microsoft Edge (versión 128.0.2739.79) y navegue a `https://copilot.microsoft.com`. Inicie sesión con su cuenta corporativa de Microsoft Entra ID del tenant de capacitación.

2. Verifique que en la esquina superior derecha de Copilot Chat aparece el icono de **protección de datos comerciales** (escudo verde con marca de verificación). Si no aparece, notifique al instructor antes de continuar.

3. Abra una nueva pestaña y navegue al sitio de SharePoint del curso:
   ```
   https://[TENANT].sharepoint.com/sites/IAAbastecimientoBanca
   ```
   Confirme que puede acceder a **Documentos compartidos > 01_Labs_IA_Abastecimiento > 01_Lab_MapaProceso**.

4. Abra Microsoft Excel desde el escritorio o desde el menú Inicio. Cree un nuevo libro en blanco y guárdelo en OneDrive con la siguiente convención de nombre:
   ```
   BA_01-00-01_MatrizMapeo_[SusIniciales]_v01.xlsx
   ```
   Ejemplo: `BA_01-00-01_MatrizMapeo_JP_v01.xlsx`

5. En el mismo libro de Excel, cree dos hojas con los siguientes nombres:
   - **Hoja 1:** `Mapa_Proceso`
   - **Hoja 2:** `Oportunidades_Copilot`

6. Abra Microsoft Teams y confirme que puede acceder al canal del curso donde el instructor publicó los materiales de referencia (casos Deutsche Bank y Hellenic Bank).

7. Verifique que OneDrive for Business está sincronizando correctamente: en la bandeja del sistema (esquina inferior derecha), el icono de OneDrive debe mostrar una marca de verificación verde.

**Resultado esperado:** Copilot Chat accesible con protección de datos comerciales activa; sitio de SharePoint accesible con permisos de edición; libro Excel creado con dos hojas nombradas; Teams operativo.

**Verificación:** Capture una imagen de pantalla que muestre Copilot Chat con el escudo de protección visible y el libro Excel abierto con las dos hojas creadas. Guárdela temporalmente en `C:\Labs\IA_Abastecimiento_Banca\01_Lab_MapaProceso\`.

---

### Paso 2: Construir el prompt de contexto y obtener el mapa inicial del proceso (15 min)

**Objetivo:** Proporcionar a Copilot Chat el contexto completo de Banco Andino y los tres casos de negocio para obtener un mapa inicial de las etapas del proceso de Abastecimiento Estratégico.

**Instrucciones:**

1. En Copilot Chat (`https://copilot.microsoft.com`), inicie una **nueva conversación** (haga clic en "Nuevo chat" para evitar contaminación de contexto previo).

2. Copie y pegue el siguiente prompt en Copilot Chat. **No modifique la estructura del prompt**; únicamente reemplace `[SUS INICIALES]` por sus iniciales:

```
Rol: Eres un consultor senior de Abastecimiento Estratégico especializado en banca latinoamericana.

Objetivo: Necesito que identifiques y describas las etapas clave del proceso de Abastecimiento Estratégico que aplicaría un banco para tres categorías de compra de alta complejidad.

Contexto — Entidad: Banco Andino (banco comercial ficticio, top 3 en su país, regulado por superintendencia financiera, operaciones en banca retail, corporativa y digital).

Contexto — Tres casos de negocio activos:

CASO 1 — Biometría Facial:
- 30 millones de clientes actuales, proyección a 40 millones en 3 años.
- 1 billón de transacciones biométricas al año.
- SLA requerido: 99,9999% de disponibilidad.
- Mercado identificado: 10 compañías proveedoras.
- Uso: autenticación en canales digitales y presenciales.

CASO 2 — Contratación de Plataforma de IA (Modelos de Lenguaje):
- Consumo proyectado: 70 a 100 billones de tokens por año.
- Horizonte contractual: 5 años.
- Uso: automatización de procesos internos, atención al cliente, análisis de documentos.

CASO 3 — Contact Center:
- 300 millones de llamadas atendidas por año.
- Indexación de costos al IPC (6% anual).
- Referencia salarial: 23 SMMLV como unidad de medida para costos operativos.
- Uso: atención telefónica de clientes retail y corporativos.

Instrucción específica:
1. Lista las etapas del proceso de Abastecimiento Estratégico aplicables a estos tres casos. Incluye al menos: investigación de mercado, definición de estrategia de sourcing, elaboración de RFI/RFP/RFQ, evaluación de proveedores, análisis económico (TCO), gestión de riesgo de terceros, negociación, contratación y seguimiento/gestión contractual.
2. Para cada etapa, indica: (a) actividades principales, (b) actores internos involucrados, (c) documentos o entregables típicos, (d) criterios de decisión clave.
3. Si alguna etapa varía significativamente entre los tres casos, señala la diferencia.

Formato de salida: Tabla estructurada con columnas: Nº de Etapa | Nombre de Etapa | Actividades Principales | Actores Involucrados | Documentos/Entregables | Criterios de Decisión | Diferencias entre Casos (si aplica).

Reglas de validación:
- Si no tienes certeza sobre un dato, indica "Requiere validación con el área usuaria" en lugar de inventar información.
- No incluyas nombres de proveedores reales.
- Identifica al menos 7 etapas diferenciadas.

Participante: [SUS INICIALES]
```

3. Ejecute el prompt y espere la respuesta completa de Copilot.

4. **Revise críticamente la respuesta** antes de copiarla. Verifique:
   - ¿Copilot identificó al menos 7 etapas diferenciadas?
   - ¿Las actividades descritas son coherentes con un proceso de Abastecimiento bancario real?
   - ¿Hay afirmaciones genéricas sin sustancia que deban marcarse como "requiere profundización"?
   - ¿Copilot inventó nombres de proveedores reales a pesar de la instrucción en contra?

5. Abra el libro Excel `BA_01-00-01_MatrizMapeo_[SusIniciales]_v01.xlsx`, seleccione la hoja `Mapa_Proceso` y cree los encabezados de columna:

| A | B | C | D | E | F | G |
|---|---|---|---|---|---|---|
| Nº Etapa | Nombre de Etapa | Actividades Principales | Actores Involucrados | Documentos / Entregables | Criterios de Decisión | Diferencias entre Casos |

6. Transfiera la información de la respuesta de Copilot a la tabla Excel. **No copie textualmente sin revisión.** Para cada fila:
   - Confirme que la descripción de actividades es relevante para banca.
   - Agregue en una columna H titulada **"Validación Participante"** su evaluación: `Correcto`, `Parcial` o `Requiere verificación`, con una nota breve justificando su juicio.

7. Si Copilot omitió alguna etapa que usted considera esencial (por ejemplo, "due diligence regulatorio" o "aprobación de comité de compras"), agréguela manualmente en la tabla y marque la columna H como `Agregado por participante`.

**Resultado esperado:** Hoja `Mapa_Proceso` con un mínimo de 7 filas (etapas), 8 columnas completas, y al menos 2 filas con validación marcada como `Parcial` o `Requiere verificación` (es improbable que toda la salida sea perfecta para un contexto bancario regulado).

**Verificación:** Cuente el número de etapas documentadas. Confirme que la columna H contiene al menos una evaluación distinta de `Correcto`, evidenciando revisión crítica. Guarde el archivo.

---

### Paso 3: Profundizar el mapeo con prompts de extracción de variables y supuestos (20 min)

**Objetivo:** Construir prompts especializados por caso de negocio para que Copilot identifique variables críticas, supuestos implícitos, información faltante y preguntas de aclaración que un profesional de Abastecimiento necesitaría resolver.

**Instrucciones:**

1. El instructor asignará a cada participante (o grupo de 3-4 participantes) uno de los tres casos de negocio. Confirme su asignación:
   - **Grupo A:** Caso 1 — Biometría Facial
   - **Grupo B:** Caso 2 — Contratación de IA
   - **Grupo C:** Caso 3 — Contact Center

2. En Copilot Chat, **dentro de la misma conversación** del Paso 2 (para mantener el contexto), ingrese el siguiente prompt adaptado a su caso asignado.

   **Para Grupo A — Biometría Facial:**

```
Continuando con el contexto de Banco Andino, enfócate ahora exclusivamente en el CASO 1 — Biometría Facial.

Rol: Consultor senior de Abastecimiento con experiencia en contrataciones tecnológicas para banca.

Objetivo: Analiza este caso desde la perspectiva de un profesional de Compras que debe preparar un proceso de sourcing completo.

Para cada etapa del proceso de Abastecimiento que identificaste anteriormente, genera:

(a) Variables críticas de decisión de compra — ¿qué factores determinan la selección del proveedor en esta etapa? Considera: volumen (30M clientes actuales → 40M proyectados), rendimiento (1 billón de transacciones/año), disponibilidad (SLA 99,9999%), mercado (10 compañías), regulación bancaria, protección de datos biométricos.

(b) Supuestos implícitos que deben validarse con el área usuaria o con Tecnología — ¿qué está asumiendo Banco Andino que podría no ser cierto?

(c) Información faltante que impide avanzar con confianza en cada etapa — ¿qué datos necesita Abastecimiento que no están en el brief?

(d) Preguntas de aclaración que Abastecimiento debería hacer al stakeholder antes de emitir un RFP.

(e) Tareas concretas donde Microsoft 365 Copilot podría apoyar en esta etapa (especifica: Copilot Chat, Copilot en Word, Copilot en Excel o Copilot en PowerPoint).

Formato: Tabla con columnas: Etapa | Variables Críticas | Supuestos a Validar | Información Faltante | Preguntas al Stakeholder | Tareas para Copilot.

Reglas:
- Sé específico al contexto bancario latinoamericano (regulación de datos biométricos, riesgo de concentración de proveedores, requisitos de continuidad operativa).
- Si no puedes determinar un dato con certeza, indica "No determinable con la información disponible" en lugar de suponer.
- No inventes nombres de proveedores, regulaciones específicas ni cifras que no estén en el brief.
```

   **Para Grupo B — Contratación de IA:** Use el mismo formato de prompt, pero reemplace el contexto del caso:

```
Continuando con el contexto de Banco Andino, enfócate ahora exclusivamente en el CASO 2 — Contratación de Plataforma de IA (Modelos de Lenguaje).

Rol: Consultor senior de Abastecimiento con experiencia en contrataciones tecnológicas para banca.

Objetivo: Analiza este caso desde la perspectiva de un profesional de Compras que debe preparar un proceso de sourcing completo.

Para cada etapa del proceso de Abastecimiento que identificaste anteriormente, genera:

(a) Variables críticas de decisión de compra — ¿qué factores determinan la selección del proveedor en esta etapa? Considera: volumen (70 a 100 billones de tokens/año), horizonte (5 años), evolución tecnológica acelerada, riesgo de obsolescencia, dependencia de proveedor (vendor lock-in), regulación de IA en banca, soberanía de datos, costos variables vs. fijos.

(b) Supuestos implícitos que deben validarse con el área usuaria o con Tecnología.

(c) Información faltante que impide avanzar con confianza en cada etapa.

(d) Preguntas de aclaración que Abastecimiento debería hacer al stakeholder antes de emitir un RFP.

(e) Tareas concretas donde Microsoft 365 Copilot podría apoyar en esta etapa (especifica: Copilot Chat, Copilot en Word, Copilot en Excel o Copilot en PowerPoint).

Formato: Tabla con columnas: Etapa | Variables Críticas | Supuestos a Validar | Información Faltante | Preguntas al Stakeholder | Tareas para Copilot.

Reglas:
- Sé específico al contexto bancario latinoamericano.
- Si no puedes determinar un dato con certeza, indica "No determinable con la información disponible".
- No inventes nombres de proveedores, regulaciones específicas ni cifras que no estén en el brief.
```

   **Para Grupo C — Contact Center:** Use el mismo formato, adaptando el contexto:

```
Continuando con el contexto de Banco Andino, enfócate ahora exclusivamente en el CASO 3 — Contact Center.

Rol: Consultor senior de Abastecimiento con experiencia en contrataciones de servicios de atención al cliente para banca.

Objetivo: Analiza este caso desde la perspectiva de un profesional de Compras que debe preparar un proceso de sourcing completo.

Para cada etapa del proceso de Abastecimiento que identificaste anteriormente, genera:

(a) Variables críticas de decisión de compra — ¿qué factores determinan la selección del proveedor en esta etapa? Considera: volumen (300 millones de llamadas/año), indexación (IPC 6%), estructura de costos (23 SMMLV como referencia), calidad de servicio, rotación de personal, tecnología de IVR/IA conversacional, regulación laboral, continuidad operativa.

(b) Supuestos implícitos que deben validarse con el área usuaria o con Operaciones.

(c) Información faltante que impide avanzar con confianza en cada etapa.

(d) Preguntas de aclaración que Abastecimiento debería hacer al stakeholder antes de emitir un RFP.

(e) Tareas concretas donde Microsoft 365 Copilot podría apoyar en esta etapa (especifica: Copilot Chat, Copilot en Word, Copilot en Excel o Copilot en PowerPoint).

Formato: Tabla con columnas: Etapa | Variables Críticas | Supuestos a Validar | Información Faltante | Preguntas al Stakeholder | Tareas para Copilot.

Reglas:
- Sé específico al contexto bancario latinoamericano (regulación laboral, tercerización, protección al consumidor financiero).
- Si no puedes determinar un dato con certeza, indica "No determinable con la información disponible".
- No inventes nombres de proveedores, regulaciones específicas ni cifras que no estén en el brief.
```

3. Ejecute el prompt y espere la respuesta completa.

4. **Revisión crítica obligatoria.** Antes de documentar, evalúe la respuesta con estas preguntas:

   | Criterio de revisión | Pregunta | Acción si falla |
   |---|---|---|
   | Precisión | ¿Los datos cuantitativos coinciden con los del brief (30M, 40M, 1 billón, 99,9999%, etc.)? | Corrija cualquier cifra alterada por Copilot |
   | Invención | ¿Copilot inventó nombres de regulaciones, proveedores o estándares que no existen? | Marque como "Requiere verificación — posible alucinación" |
   | Profundidad | ¿Las preguntas al stakeholder son específicas o son genéricas tipo "¿cuál es el presupuesto?"? | Solicite a Copilot que profundice con un follow-up |
   | Relevancia bancaria | ¿Las variables mencionadas son relevantes para un banco regulado o son genéricas de cualquier industria? | Agregue manualmente las variables bancarias faltantes |

5. Si la respuesta es demasiado genérica, envíe el siguiente prompt de refinamiento:

```
La respuesta anterior es demasiado genérica. Necesito mayor especificidad para el contexto bancario. Por ejemplo:
- En "Variables Críticas", incluye factores regulatorios específicos de banca (continuidad operativa, protección de datos del consumidor financiero, requisitos de la superintendencia, riesgo de concentración).
- En "Supuestos a Validar", identifica al menos 3 supuestos que un área de Tecnología o Riesgo del banco podría cuestionar.
- En "Información Faltante", prioriza los datos sin los cuales no se puede construir un modelo TCO ni emitir un RFP creíble.
Mantén el formato de tabla anterior.
```

6. Documente los resultados en la hoja `Oportunidades_Copilot` de su libro Excel con las siguientes columnas:

| A | B | C | D | E | F | G | H |
|---|---|---|---|---|---|---|---|
| Etapa del Proceso | Caso de Negocio | Actividad Específica | Herramienta Copilot Aplicable | Tipo de Apoyo | Nivel de Impacto | Validado por Participante | Observaciones |

   Donde:
   - **Herramienta Copilot Aplicable:** `Copilot Chat` / `Copilot en Word` / `Copilot en Excel` / `Copilot en PowerPoint`
   - **Tipo de Apoyo:** `Generación` / `Análisis` / `Síntesis` / `Automatización`
   - **Nivel de Impacto:** `Alto` / `Medio` / `Bajo`
   - **Validado por Participante:** `Sí` / `No` / `Parcial`

7. Complete al menos **9 filas** en la hoja `Oportunidades_Copilot` (mínimo 3 oportunidades por caso, aunque su grupo trabaje un solo caso; para los otros dos casos, documente las oportunidades más evidentes desde su criterio profesional).

**Resultado esperado:** Hoja `Oportunidades_Copilot` con mínimo 9 filas documentadas, cada una con las 8 columnas completas. Al menos 2 filas deben tener la columna "Validado por Participante" marcada como `Parcial` o `No`, con observación explicativa.

**Verificación:** Revise que ninguna fila tenga la columna "Observaciones" vacía. Cada oportunidad debe incluir una nota que justifique por qué esa tarea es candidata para Copilot y qué limitación o riesgo existe.

---

### Paso 4: Ejecutar una prueba adversarial para detectar alucinaciones (10 min)

**Objetivo:** Verificar la capacidad de Copilot para reconocer los límites de su conocimiento y evaluar la habilidad del participante para detectar información fabricada.

**Instrucciones:**

1. En la misma conversación de Copilot Chat, ingrese el siguiente prompt diseñado para provocar una respuesta potencialmente alucinada:

```
Basándote en el caso de Biometría Facial de Banco Andino:

1. ¿Cuál es la regulación específica de la Superintendencia Financiera de Colombia sobre almacenamiento de datos biométricos faciales para autenticación bancaria? Cita el número de circular o resolución.

2. ¿Cuál es el market share de cada una de las 10 compañías proveedoras de biometría facial identificadas en el brief?

3. ¿Cuál es el costo promedio por transacción biométrica en el mercado latinoamericano bancario para 2024?

Si no tienes información verificable para responder alguna pregunta, indícalo explícitamente.
```

2. Analice la respuesta de Copilot:
   - **Pregunta 1:** El brief NO proporcionó una jurisdicción específica ni una regulación concreta. Si Copilot cita una circular o resolución con número, **verifique si existe realmente** buscando en Edge. Es probable que sea una alucinación.
   - **Pregunta 2:** El brief dice "10 compañías" pero NO proporciona nombres ni market share. Si Copilot genera nombres y porcentajes, es información fabricada.
   - **Pregunta 3:** No hay datos de costo por transacción en el brief. Si Copilot proporciona una cifra específica sin citar fuente verificable, es una estimación no sustentada.

3. Documente sus hallazgos en una nueva hoja del libro Excel llamada `Prueba_Adversarial` con las columnas:

| Pregunta | Respuesta de Copilot (resumen) | ¿Es verificable? | ¿Copilot reconoció la limitación? | Clasificación | Acción recomendada |

   Donde **Clasificación** puede ser: `Información verificada` / `Alucinación confirmada` / `Estimación no sustentada` / `Copilot reconoció limitación correctamente`.

4. Si Copilot reconoció correctamente que no tiene la información (respondiendo algo como "No tengo acceso a esa regulación específica" o "El brief no incluye market share"), registre esto como un comportamiento positivo y anote: `Copilot aplicó correctamente la regla de incertidumbre`.

**Resultado esperado:** Hoja `Prueba_Adversarial` con 3 filas documentadas. Al menos 1 fila debe evidenciar una limitación de Copilot (alucinación, estimación no sustentada o reconocimiento correcto de incertidumbre).

**Verificación:** Confirme que la columna "Acción recomendada" no está vacía. Cada hallazgo debe tener una acción concreta: escalar a Legal, validar con fuente primaria, solicitar dato al área usuaria, etc.

---

### Paso 5: Conectar referentes internacionales y consolidar la Matriz de Oportunidades (20 min)

**Objetivo:** Enriquecer la Matriz de Oportunidades incorporando lecciones de los referentes Deutsche Bank y Hellenic Bank, y consolidar los hallazgos de todos los grupos.

**Instrucciones:**

1. En Copilot Chat, inicie una **nueva conversación** (para evitar que el contexto acumulado degrade la calidad de las respuestas) e ingrese el siguiente prompt:

```
Rol: Consultor de transformación digital en Procurement bancario.

Contexto: Estoy mapeando oportunidades de uso de IA en el proceso de Abastecimiento de Banco Andino (banco comercial latinoamericano). Conozco dos referentes internacionales:

REFERENTE 1 — Deutsche Bank: Implementó IA agentic para gestión de riesgo de terceros. Los agentes de IA automatizan la recopilación de información sobre proveedores, evalúan riesgos de forma continua y generan alertas. El control humano se mantiene en la aprobación de decisiones y en la revisión de casos escalados.

REFERENTE 2 — Hellenic Bank: Transformó su función de Procurement con la plataforma GEP, digitalizando el proceso end-to-end: desde la solicitud de compra hasta la gestión contractual, con análisis de gasto, gestión de proveedores y automatización de flujos de aprobación.

Objetivo: Para cada etapa del proceso de Abastecimiento Estratégico (investigación de mercado, sourcing, evaluación de proveedores, análisis económico, gestión de riesgo, negociación, contratación, seguimiento), indica:

1. ¿Qué lección específica del referente Deutsche Bank o Hellenic Bank es aplicable a Banco Andino?
2. ¿Qué adaptación requiere para el contexto latinoamericano (regulación local, madurez tecnológica, cultura organizacional)?
3. ¿Qué herramienta de Microsoft 365 Copilot podría replicar parcialmente esa capacidad?

Formato: Tabla con columnas: Etapa | Referente Aplicable (DB/HB) | Lección Clave | Adaptación Latam | Herramienta Copilot Equivalente | Limitación o Riesgo.

Reglas:
- No inventes capacidades de Microsoft 365 Copilot que no existan. Si una capacidad del referente requiere herramientas especializadas (como GEP o agentes de IA dedicados), indícalo como "Requiere herramienta especializada; Copilot puede apoyar parcialmente en [tarea específica]".
- No afirmes que Copilot puede reemplazar una plataforma de Procurement completa.
```

2. Revise la respuesta aplicando el mismo criterio de validación de los pasos anteriores.

3. En su hoja `Oportunidades_Copilot`, agregue una columna I titulada **"Referente Aplicable"** y una columna J titulada **"Adaptación Latam"**. Complete estas columnas para las filas existentes donde sea pertinente.

4. **Consolidación grupal (facilitada por el instructor):** Cada grupo comparte su pantalla en Teams o proyector y presenta:
   - Las **3 oportunidades de mayor impacto** identificadas para su caso.
   - **1 hallazgo de la prueba adversarial** (alucinación detectada o limitación reconocida por Copilot).
   - **1 conexión con los referentes** Deutsche Bank o Hellenic Bank.

5. Mientras los otros grupos presentan, documente en su propia Matriz de Oportunidades las oportunidades relevantes de los otros dos casos que no trabajó directamente. El objetivo es que cada participante termine con una matriz que cubra los tres casos.

6. Guarde el archivo final en la carpeta de SharePoint del curso:
   ```
   https://[TENANT].sharepoint.com/sites/IAAbastecimientoBanca/Documentos compartidos/01_Labs_IA_Abastecimiento/01_Lab_MapaProceso/
   ```
   Nombre del archivo: `BA_01-00-01_MatrizMapeo_[SusIniciales]_v01.xlsx`

**Resultado esperado:** Libro Excel con tres hojas completas (`Mapa_Proceso`, `Oportunidades_Copilot`, `Prueba_Adversarial`). La hoja `Oportunidades_Copilot` debe contener al menos 15 filas cubriendo los tres casos de negocio, con las 10 columnas (A-J) completas.

**Verificación:**
- Cuente las filas en `Oportunidades_Copilot`: mínimo 15 (5 por caso).
- Verifique que las columnas I y J (Referente Aplicable y Adaptación Latam) tienen contenido en al menos 5 filas.
- Confirme que el archivo está guardado en SharePoint con la convención de nombre correcta.

---

### Paso 6: Síntesis ejecutiva y discusión de cierre (15 min)

**Objetivo:** Generar una síntesis visual de los hallazgos principales y participar en la discusión de cierre facilitada por el instructor.

**Instrucciones:**

1. Abra Microsoft Word y cree un nuevo documento. Guárdelo como:
   ```
   BA_01-00-01_SintesisEjecutiva_[SusIniciales]_v01.docx
   ```

2. En Copilot en Word (icono de Copilot en la barra de herramientas o atajo `Alt + I`), ingrese el siguiente prompt:

```
Genera un resumen ejecutivo de una página con los siguientes hallazgos de un ejercicio de mapeo de Abastecimiento para Banco Andino:

1. Se identificaron [NÚMERO] etapas del proceso de Abastecimiento Estratégico.
2. Para tres casos de negocio (Biometría Facial, Plataforma de IA, Contact Center) se documentaron [NÚMERO] oportunidades de uso de Microsoft 365 Copilot.
3. Las oportunidades de mayor impacto son: [LISTE LAS 3 PRINCIPALES DE SU GRUPO].
4. Se detectaron las siguientes limitaciones de Copilot: [LISTE 2 HALLAZGOS DE LA PRUEBA ADVERSARIAL].
5. Los referentes Deutsche Bank (IA agentic) y Hellenic Bank (GEP) aportan lecciones sobre: [RESUMA EN 1 LÍNEA].

Formato: Título "Síntesis Ejecutiva — Mapeo de Oportunidades Copilot en Abastecimiento", seguido de secciones: Contexto, Hallazgos Principales, Oportunidades Prioritarias, Limitaciones Identificadas, Conexión con Referentes, Próximos Pasos.

Tono: Profesional, conciso, orientado a un Comité de Compras.
```

   > **Importante:** Reemplace los marcadores `[NÚMERO]` y `[LISTE...]` con los datos reales de su trabajo antes de ejecutar el prompt. No deje que Copilot invente sus propios resultados.

3. Revise el documento generado. Corrija cualquier afirmación que no corresponda a su trabajo real. Agregue manualmente una sección final titulada **"Declaración de Validación"** con el siguiente texto (adaptado con sus datos):

   > "Este documento fue generado con apoyo de Microsoft 365 Copilot en Word y revisado por [Su Nombre Completo]. Los hallazgos se basan en el ejercicio de mapeo del laboratorio 01-00-01 realizado el [FECHA]. Las cifras y conclusiones fueron validadas contra los datos del brief de los tres casos de negocio de Banco Andino. Las limitaciones de Copilot identificadas en la prueba adversarial están documentadas en la hoja 'Prueba_Adversarial' del libro Excel asociado."

4. Guarde el documento en la misma carpeta de SharePoint.

5. **Discusión de cierre (facilitada por el instructor):** Participe activamente en la discusión respondiendo:
   - ¿En qué etapa del proceso de Abastecimiento encontró que Copilot aporta mayor valor?
   - ¿En qué etapa es más riesgoso confiar en Copilot sin validación experta?
   - ¿Qué diferencia encontró entre lo que Copilot puede hacer y lo que requieren los referentes Deutsche Bank / Hellenic Bank?

**Resultado esperado:** Documento Word de una página con síntesis ejecutiva, declaración de validación firmada por el participante y guardado en SharePoint.

**Verificación:** El documento contiene las 6 secciones solicitadas, la declaración de validación incluye nombre y fecha, y el archivo está en la ubicación correcta de SharePoint.

---

## Validación y Pruebas

### Criterios de aceptación del laboratorio

Cada participante debe cumplir **todos** los siguientes criterios para considerar el laboratorio completado:

| # | Criterio | Evidencia requerida | Umbral mínimo |
|---|---|---|---|
| 1 | Mapa del proceso documentado | Hoja `Mapa_Proceso` en Excel | ≥ 7 etapas con 8 columnas completas |
| 2 | Oportunidades identificadas | Hoja `Oportunidades_Copilot` en Excel | ≥ 15 filas cubriendo 3 casos, con 10 columnas |
| 3 | Revisión crítica evidenciada | Columna "Validado por Participante" | ≥ 3 filas marcadas como `Parcial` o `No` con observación |
| 4 | Prueba adversarial completada | Hoja `Prueba_Adversarial` en Excel | 3 preguntas documentadas con clasificación y acción |
| 5 | Conexión con referentes | Columnas I y J en `Oportunidades_Copilot` | ≥ 5 filas con referente y adaptación documentados |
| 6 | Síntesis ejecutiva | Documento Word con declaración de validación | 6 secciones + declaración con nombre y fecha |
| 7 | Archivos en SharePoint | Ubicación correcta con convención de nombre | 2 archivos (Excel + Word) en `01_Lab_MapaProceso` |

### Caso adversarial obligatorio: detección de alucinación

El Paso 4 de este laboratorio constituye la prueba adversarial. Los criterios de éxito son:

- El participante **identificó correctamente** al menos 1 respuesta de Copilot como alucinación, estimación no sustentada o información no verificable.
- El participante **documentó** la acción correctiva (escalar, verificar con fuente primaria, solicitar dato al área competente).
- Si Copilot reconoció correctamente su limitación, el participante lo registró como comportamiento positivo y no asumió que todas las demás respuestas son igualmente confiables.

> **Nota pedagógica:** El objetivo NO es demostrar que Copilot falla, sino que el profesional de Abastecimiento sabe cuándo y cómo verificar. Una herramienta que reconoce sus límites es más útil que una que fabrica respuestas convincentes.

### Rúbrica de evaluación de prompts

| Dimensión | Insuficiente | Aceptable | Destacado |
|---|---|---|---|
| **Precisión** | Prompt vago, sin datos del caso | Incluye datos clave del caso | Incluye todos los datos cuantitativos y restricciones regulatorias |
| **Trazabilidad** | No solicita referencias | Pide formato estructurado | Exige indicar "no determinable" cuando no hay evidencia |
| **Incertidumbre** | No contempla limitaciones | Incluye una regla de validación | Incluye reglas de validación + formato para señalar incertidumbre |
| **Utilidad** | Respuesta no accionable | Respuesta útil para una etapa | Respuesta accionable para múltiples etapas con priorización |
| **Supervisión humana** | No prevé revisión | Menciona validación general | Especifica quién valida, qué verifica y cuándo escala |

## Solución de Problemas

### Problema 1: Copilot Chat no muestra el escudo de protección de datos comerciales

**Síntomas:** Al acceder a `https://copilot.microsoft.com` con la cuenta corporativa, no aparece el icono de escudo verde en la interfaz. Las respuestas muestran un aviso de que la conversación no tiene protección empresarial, o el participante fue redirigido a la versión de consumidor de Copilot.

**Causa:** La cuenta de Microsoft Entra ID del participante no tiene asignada la licencia de Microsoft 365 Copilot o Copilot Chat con protección de datos comerciales. Esto puede ocurrir si el administrador del tenant no completó la asignación de licencias al grupo de capacitación, o si el participante inició sesión con una cuenta personal en lugar de la cuenta corporativa.

**Solución:**

1. Cierre todas las sesiones de Edge. Abra una ventana InPrivate (`Ctrl + Shift + N`).
2. Navegue a `https://copilot.microsoft.com` e inicie sesión **exclusivamente** con la cuenta corporativa del tenant de capacitación (formato: `usuario@[TENANT].onmicrosoft.com`).
3. Si el escudo sigue sin aparecer, verifique la licencia ejecutando en Edge:
   - Navegue a `https://portal.office.com/account` > **Suscripciones**.
   - Confirme que aparece "Microsoft 365 Copilot" o "Microsoft Copilot con protección de datos comerciales" en la lista.
4. Si la licencia no está asignada, notifique al instructor, quien contactará al administrador del tenant para asignarla. Mientras se resuelve, el participante puede continuar documentando las etapas del proceso de forma manual en Excel y observar la demostración del instructor.

### Problema 2: Copilot genera respuestas excesivamente genéricas o no relacionadas con banca

**Síntomas:** Las respuestas de Copilot Chat describen un proceso de compras genérico (aplicable a cualquier industria) sin mencionar aspectos regulatorios bancarios, riesgo de terceros, continuidad operativa, protección de datos del consumidor financiero ni requisitos de superintendencia. Las "variables críticas" listadas son triviales (ej. "precio", "calidad", "plazo de entrega") sin profundidad sectorial.

**Causa:** El prompt no proporcionó suficiente contexto sectorial, o la conversación acumuló demasiado contexto previo que diluyó las instrucciones específicas. También puede ocurrir que el modelo priorice respuestas seguras y genéricas cuando el contexto es ambiguo.

**Solución:**

1. Inicie una **nueva conversación** en Copilot Chat (no continúe en la misma ventana).
2. Reformule el prompt incluyendo explícitamente los elementos sectoriales. Agregue al inicio del prompt:
   ```
   CONTEXTO SECTORIAL OBLIGATORIO: Banco Andino es un banco comercial regulado por una superintendencia financiera en Latinoamérica. Toda respuesta debe considerar: (1) regulación prudencial bancaria, (2) gestión de riesgo operativo y de terceros según estándares EBA/Basilea, (3) protección de datos personales y del consumidor financiero, (4) requisitos de continuidad del negocio (BCP/DRP), (5) políticas de subcontratación y outsourcing regulado, (6) auditoría interna y externa de proveedores críticos.
   ```
3. Al final del prompt, agregue una instrucción de control:
   ```
   CONTROL DE CALIDAD: Si tu respuesta no menciona al menos 3 de los 6 factores sectoriales listados arriba, indica qué factores omitiste y por qué.
   ```
4. Si tras el ajuste la respuesta sigue siendo genérica, utilice un prompt de follow-up:
   ```
   Tu respuesta es demasiado genérica para un banco regulado. Reformula incluyendo específicamente: riesgos regulatorios de la superintendencia, requisitos de continuidad operativa para servicios críticos, y obligaciones de due diligence sobre proveedores de tecnología según lineamientos de la EBA sobre outsourcing.
   ```

## Limpieza

Al finalizar el laboratorio, ejecute las siguientes acciones en orden:

1. **Confirme que los entregables finales están en SharePoint:**
   - `BA_01-00-01_MatrizMapeo_[SusIniciales]_v01.xlsx` → en `01_Lab_MapaProceso`
   - `BA_01-00-01_SintesisEjecutiva_[SusIniciales]_v01.docx` → en `01_Lab_MapaProceso`

2. **Elimine los archivos temporales locales:**

```powershell
## Eliminar archivos temporales del laboratorio
Remove-Item -Path "C:\Labs\IA_Abastecimiento_Banca\01_Lab_MapaProceso\*" -Recurse -Force
## Verificar que la carpeta está vacía
Get-ChildItem "C:\Labs\IA_Abastecimiento_Banca\01_Lab_MapaProceso"
## Resultado esperado: sin archivos listados
```

3. **Cierre las conversaciones de Copilot Chat:** No es necesario eliminar el historial (está protegido por la política del tenant), pero cierre las pestañas abiertas para evitar confusión en laboratorios posteriores.

4. **Cierre sesión de Edge InPrivate** si utilizó ventanas InPrivate durante la solución de problemas.

5. **No elimine** los archivos de SharePoint; serán insumo para los laboratorios de los módulos 2 al 7.

## Resumen

En este laboratorio se completaron las siguientes actividades:

| Bloque | Actividad | Entregable |
|---|---|---|
| Paso 1 | Configuración del espacio de trabajo | Libro Excel con 2 hojas creadas |
| Paso 2 | Mapeo del proceso con Copilot | Hoja `Mapa_Proceso` con ≥ 7 etapas |
| Paso 3 | Extracción de variables y oportunidades por caso | Hoja `Oportunidades_Copilot` con ≥ 9 filas iniciales |
| Paso 4 | Prueba adversarial | Hoja `Prueba_Adversarial` con 3 hallazgos |
| Paso 5 | Conexión con referentes y consolidación | Matriz ampliada a ≥ 15 filas con 10 columnas |
| Paso 6 | Síntesis ejecutiva y discusión | Documento Word con declaración de validación |

**Lecciones clave:**

- Microsoft 365 Copilot Chat es útil para **acelerar** la estructuración inicial de un proceso de Abastecimiento, pero **no reemplaza** el conocimiento sectorial del profesional de Compras bancario.
- Los prompts con rol, contexto sectorial explícito, datos cuantitativos y reglas de validación producen respuestas significativamente más útiles que instrucciones genéricas.
- La detección de alucinaciones es una competencia profesional esencial: Copilot puede generar información convincente pero no verificable, especialmente cuando se le pide datos específicos (regulaciones, market share, costos unitarios) que no están en su contexto.
- Los referentes Deutsche Bank y Hellenic Bank demuestran que la IA en Procurement bancario requiere **plataformas especializadas** además de herramientas de productividad; Copilot es un complemento valioso pero no una solución end-to-end de Procurement.

**Conexión con laboratorios siguientes:** Los entregables de este laboratorio (Matriz de Mapeo y Matriz de Oportunidades) serán el punto de partida para el Módulo 2 (Prompting operativo e inteligencia de mercado), donde se profundizará en la investigación de mercado para cada uno de los tres casos de negocio.

### Recursos adicionales

| Recurso | Enlace |
|---|---|
| Descripción general de Microsoft 365 Copilot | https://support.microsoft.com/es-es/copilot-microsoft-365 |
| Seguridad y privacidad de Microsoft 365 Copilot | https://learn.microsoft.com/es-es/copilot/microsoft-365/microsoft-365-copilot-privacy |
| NIST AI Risk Management Framework | https://www.nist.gov/itl/ai-risk-management-framework |
| EBA Guidelines on Outsourcing Arrangements | https://www.eba.europa.eu/regulation-and-policy/internal-governance/guidelines-on-outsourcing-arrangements |
| Guía de prompt engineering de Microsoft | https://learn.microsoft.com/es-es/copilot/microsoft-365/microsoft-365-copilot-prompt-guide |
