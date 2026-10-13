# Práctica: Orquestar un workflow de Abastecimiento con Microsoft 365 Copilot

## Metadatos

| Campo | Valor |
|---|---|
| **Duración** | 105 minutos |
| **Complejidad** | Alta |
| **Nivel Bloom** | Aplicar (Apply) |
| **Caso de negocio** | Renovación del servicio de ciberseguridad gestionada — Banco Andino (datos sintéticos) |
| **Aplicaciones M365** | Copilot Chat, Word, Excel, PowerPoint, Outlook, Teams |

## Descripción General

Este laboratorio integrador conecta todas las fases de un proceso de Abastecimiento estratégico dentro de un único workflow asistido por Microsoft 365 Copilot. Los participantes tomarán el caso de renovación del servicio de ciberseguridad gestionada del Banco Andino y los entregables generados en laboratorios previos (market scan, RFP/RFQ, comparativo de proveedores, modelo de TCO, análisis de riesgos) para ejecutar cinco bloques secuenciales: consolidación de contexto en Copilot Chat, preparación de documentos de sourcing en Word, análisis económico en Excel, presentación ejecutiva en PowerPoint, y comunicaciones con proveedores y seguimiento en Outlook y Teams. El criterio profesional y las decisiones de adjudicación permanecen exclusivamente en los participantes; Copilot actúa como acelerador bajo supervisión humana.

## Objetivos de Aprendizaje

Al completar este laboratorio, serás capaz de:

- [ ] Integrar Microsoft 365 Copilot en un flujo de Abastecimiento de principio a fin, conectando market scan, RFP/RFQ, evaluación de propuestas, análisis económico, gestión de riesgos y negociación dentro de un workflow coherente.
- [ ] Construir y mantener contexto conversacional en Copilot Chat para consolidar investigación de mercado, perfil del negociador y estado del proceso, referenciando archivos almacenados en OneDrive/SharePoint.
- [ ] Generar, enriquecer y validar entregables de Abastecimiento en Word, Excel, PowerPoint, Outlook y Teams, aplicando criterio profesional para corregir, contextualizar y verificar cada salida de Copilot.
- [ ] Detectar al menos una limitación concreta de Copilot (alucinación, dato no sustentado, inferencia presentada como hecho) durante el workflow y documentar la corrección aplicada.
- [ ] Producir un conjunto de artefactos trazables y reutilizables (ficha de negociación, documento de recomendación, modelo TCO actualizado, presentación ejecutiva, correos de adjudicación y lista de tareas) almacenados en SharePoint con la convención de nombres del curso.

## Prerrequisitos

### Conocimientos previos

| Requisito | Detalle |
|---|---|
| Laboratorios previos del curso | Haber completado o revisado los laboratorios de los módulos 1 al 6, o disponer de los archivos de respaldo provistos por el instructor en la carpeta `00_Plantillas_Fuentes` |
| Abastecimiento estratégico | Comprensión de procesos de sourcing, RFP/RFQ, evaluación de propuestas, TCO y negociación |
| Microsoft 365 intermedio | Manejo funcional de Word, Excel, PowerPoint, Outlook y Teams |
| Prompting para Copilot | Familiaridad con la estructura de instrucciones (rol, objetivo, contexto, fuentes, criterios de salida, reglas de validación) practicada en módulos anteriores |

### Acceso y licencias

| Requisito | Verificación |
|---|---|
| Cuenta Microsoft Entra ID en el tenant de laboratorio | Iniciar sesión en https://m365.cloud.microsoft y confirmar acceso al portal |
| Licencia Microsoft 365 Copilot (add-on) activa | Abrir https://m365.cloud.microsoft/chat y verificar que Copilot Chat responde consultas |
| Acceso al sitio SharePoint del curso | Navegar a `https://[TENANT].sharepoint.com/sites/IAAbastecimientoBanca` y confirmar permisos de edición en la biblioteca `Documentos compartidos` |
| Archivos del caso sincronizados en OneDrive | Verificar que la carpeta `01_Labs_IA_Abastecimiento` contiene los entregables de laboratorios previos o los archivos de respaldo |
| Copilot visible en aplicaciones de escritorio | Abrir Word, Excel y PowerPoint y confirmar que el botón **Copilot** aparece en la cinta de opciones (pestaña **Inicio**) |

## Entorno de Laboratorio

### Hardware mínimo

| Componente | Especificación |
|---|---|
| Procesador | 64 bits, 4 núcleos o superior |
| RAM | 16 GB recomendados (8 GB mínimo) |
| Almacenamiento libre | 10 GB para sincronización de OneDrive y archivos temporales |
| Pantalla | 1920 × 1080 mínimo; se recomienda monitor adicional |
| Red | 20 Mbps descarga / 5 Mbps carga; acceso HTTPS a dominios Microsoft 365 |
| Audio | Auriculares con micrófono (opcional, para simulación en Teams) |

### Software requerido

| Aplicación | Versión / Build | Notas |
|---|---|---|
| Windows 11 Pro | 23H2, Build 22631.4169 | Administrado por la organización |
| Microsoft Edge | 128.0.2739.79 | Navegador para Copilot Chat |
| Microsoft 365 Apps for Enterprise | Versión 2408, Build 17928.20156 | Incluye Word, Excel, PowerPoint, Outlook |
| Microsoft Teams | Cliente de escritorio, canal de actualización administrado por el tenant | Versión SaaS |
| Microsoft 365 Copilot | Servicio SaaS (add-on de licencia) | Sin versión fija publicable |
| Microsoft Copilot Chat | Servicio SaaS en https://m365.cloud.microsoft/chat | Sin versión fija publicable |
| OneDrive for Business | Versión 24.091.0507.0001 | Sincronización de archivos del workflow |

### Archivos de entrada del laboratorio

Los siguientes archivos deben estar disponibles en OneDrive o en la carpeta compartida de SharePoint **antes** de iniciar el laboratorio. Si el participante completó los laboratorios previos, utilizará sus propios entregables. Si no, el instructor proporcionará archivos de respaldo en `00_Plantillas_Fuentes`.

| Archivo de respaldo | Descripción | Ubicación en SharePoint |
|---|---|---|
| `BA_02_MarketScan_Respaldo_v01.docx` | Resumen de investigación de mercado de ciberseguridad gestionada | `00_Plantillas_Fuentes` |
| `BA_03_RFP_Ciberseguridad_Respaldo_v01.docx` | Documento RFP con requisitos técnicos y comerciales | `00_Plantillas_Fuentes` |
| `BA_04_ComparativoProveedores_Respaldo_v01.xlsx` | Matriz de evaluación de 3 proveedores con scoring | `00_Plantillas_Fuentes` |
| `BA_04_TCO_Modelo_Respaldo_v01.xlsx` | Modelo de TCO a 3 años con costos directos e indirectos | `00_Plantillas_Fuentes` |
| `BA_05_AnalisisRiesgo_Respaldo_v01.docx` | Análisis de riesgos contractuales y operativos | `00_Plantillas_Fuentes` |
| `BA_06_MinutaNegociacion_Respaldo_v01.docx` | Minuta simulada de primera reunión de negociación | `00_Plantillas_Fuentes` |

### Preparación del directorio local

Ejecutar en una ventana de PowerShell antes de iniciar:

```powershell
## Crear directorio local temporal para el laboratorio
New-Item -ItemType Directory -Path "C:\Labs\IA_Abastecimiento_Banca\07_Workflow" -Force

## Verificar acceso a OneDrive sincronizado
Test-Path "$env:OneDrive\01_Labs_IA_Abastecimiento"
```

El comando `Test-Path` debe devolver `True`. Si devuelve `False`, sincronizar manualmente la carpeta desde SharePoint antes de continuar.

## Instrucciones Paso a Paso

> **Nota sobre tiempos:** Los tiempos indicados son orientativos. El instructor puede ajustarlos según el ritmo del grupo. Los cinco bloques suman aproximadamente 95 minutos de trabajo activo más 10 minutos de cierre reflexivo.

---

### Paso 1: Preparar el entorno y verificar archivos de entrada (~5 min)

**Objetivo:** Confirmar que todos los archivos del caso, las aplicaciones y Copilot están operativos antes de iniciar el workflow.

**Instrucciones:**

1. Abrir Microsoft Edge y navegar a `https://[TENANT].sharepoint.com/sites/IAAbastecimientoBanca/Documentos%20compartidos/01_Labs_IA_Abastecimiento`.

2. Verificar que existen los archivos del caso de ciberseguridad (propios o de respaldo). Anotar los nombres exactos de los archivos que se utilizarán en el workflow:
   - Market scan (`.docx`)
   - RFP/RFQ (`.docx`)
   - Comparativo de proveedores (`.xlsx`)
   - Modelo de TCO (`.xlsx`)
   - Análisis de riesgos (`.docx`)
   - Minuta de negociación (`.docx`)

3. Abrir cada una de las siguientes aplicaciones e iniciar sesión con la cuenta del tenant de laboratorio. Confirmar que el botón **Copilot** es visible:
   - Microsoft Word → Abrir un documento en blanco → Verificar botón Copilot en cinta.
   - Microsoft Excel → Abrir un libro en blanco → Verificar botón Copilot en cinta.
   - Microsoft PowerPoint → Abrir presentación en blanco → Verificar botón Copilot en cinta.
   - Microsoft Outlook → Verificar que Copilot aparece al redactar un nuevo correo.
   - Microsoft Teams → Abrir la aplicación y confirmar acceso al equipo del curso.

4. Navegar a `https://m365.cloud.microsoft/chat` y enviar el mensaje de prueba:

   ```text
   ¿Puedes acceder a mis archivos de OneDrive? Lista los últimos 3 archivos modificados.
   ```

5. Confirmar que Copilot Chat devuelve nombres de archivos reales de OneDrive. Si no lo hace, verificar la sincronización y los permisos.

6. Crear la carpeta local temporal:

   ```powershell
   New-Item -ItemType Directory -Path "C:\Labs\IA_Abastecimiento_Banca\07_Workflow" -Force
   ```

**Resultado esperado:** Todas las aplicaciones abiertas con Copilot funcional; archivos del caso identificados y accesibles; Copilot Chat conectado a los archivos de OneDrive.

**Verificación:** El participante tiene una lista escrita (en papel o archivo local) con los 6 nombres de archivo que usará en el workflow. Copilot Chat devolvió al menos un nombre de archivo real.

---

### Paso 2: Consolidar contexto e investigación de mercado en Copilot Chat — BLOQUE 1 (~20 min)

**Objetivo:** Utilizar Copilot Chat para sintetizar la investigación de mercado previa, construir el perfil del negociador (fortalezas, debilidades, BATNA, objetivos) y generar una ficha de preparación de negociación estructurada.

**Instrucciones:**

1. Abrir una **nueva conversación** en Copilot Chat (`https://m365.cloud.microsoft/chat`). Titular mentalmente esta conversación como "Consolidación de contexto — Ciberseguridad".

2. Enviar la siguiente instrucción para establecer el contexto del workflow. **Adaptar** los nombres de archivo a los archivos reales del participante:

   ```text
   Actúa como analista senior de Abastecimiento estratégico del Banco Andino,
   una entidad financiera ficticia.

   Objetivo: Consolidar toda la información disponible sobre el proceso de
   renovación del servicio de ciberseguridad gestionada para preparar la
   negociación final con el proveedor recomendado.

   Fuentes autorizadas (archivos en mi OneDrive):
   - Market scan: [NOMBRE_ARCHIVO_MARKET_SCAN.docx]
   - RFP: [NOMBRE_ARCHIVO_RFP.docx]
   - Comparativo de proveedores: [NOMBRE_ARCHIVO_COMPARATIVO.xlsx]
   - Modelo de TCO: [NOMBRE_ARCHIVO_TCO.xlsx]
   - Análisis de riesgos: [NOMBRE_ARCHIVO_RIESGOS.docx]
   - Minuta de negociación: [NOMBRE_ARCHIVO_MINUTA.docx]

   Tarea 1: Resume el estado actual del proceso de sourcing en una tabla con
   las columnas: Fase | Estado | Hallazgo principal | Documento fuente.
   Incluye las fases: investigación de mercado, emisión de RFP, evaluación
   de propuestas, análisis TCO, análisis de riesgos, negociación.

   Reglas:
   - Usa SOLO información de los documentos listados.
   - Si una fase no tiene información disponible, indica "Sin evidencia en
     documentos proporcionados".
   - Distingue hechos documentados de inferencias.
   - No inventes datos, proveedores ni cifras.
   ```

3. Revisar la tabla generada. Para cada fila, verificar:
   - ¿El hallazgo corresponde realmente al documento citado?
   - ¿Hay alguna inferencia presentada como hecho?
   - ¿Falta alguna fase o información relevante?

   Anotar al menos **una corrección necesaria** (puede ser un dato impreciso, una fuente incorrecta o una omisión).

4. Enviar una segunda instrucción para construir el perfil del negociador:

   ```text
   Tarea 2: Con base en los mismos documentos, elabora el perfil de
   preparación del negociador con la siguiente estructura:

   A. FORTALEZAS DEL BANCO ANDINO como comprador:
      - Listar con evidencia del documento fuente.

   B. DEBILIDADES O DEPENDENCIAS:
      - Listar con evidencia; indicar nivel de riesgo (alto/medio/bajo).

   C. BATNA (Mejor Alternativa a un Acuerdo Negociado):
      - Describir la alternativa más viable si no se renueva con el
        proveedor actual. Basar en el comparativo de proveedores.

   D. OBJETIVOS DE NEGOCIACIÓN (máximo 5):
      - Priorizar por impacto para el banco.

   E. LÍNEAS ROJAS (condiciones no negociables):
      - Derivar de los requisitos del RFP y del análisis de riesgos.

   Formato: Secciones con viñetas. Cada punto debe citar el documento fuente.
   Si no hay evidencia para un elemento, escribir "REQUIERE VALIDACIÓN HUMANA".
   ```

5. Revisar el perfil generado. Evaluar críticamente:
   - ¿El BATNA es realista o Copilot inventó una alternativa sin sustento?
   - ¿Las líneas rojas reflejan los requisitos reales del RFP?
   - ¿Los objetivos son coherentes con el contexto bancario?

   Corregir al menos **dos elementos** del perfil directamente en la conversación, indicando a Copilot la corrección y la razón.

6. Solicitar la ficha de negociación consolidada:

   ```text
   Tarea 3: Genera una ficha de negociación ejecutiva con cuatro bloques:

   1. POSICIÓN ACTUAL: Resumen en 3-4 oraciones del estado del proceso.
   2. EVIDENCIA CLAVE: Los 5 datos más relevantes para la negociación,
      con fuente documental.
   3. RIESGOS E INCERTIDUMBRES: Los 3 principales riesgos identificados
      y qué información falta para mitigarlos.
   4. PREGUNTAS ABIERTAS PARA EL PROVEEDOR: 5 preguntas concretas que
      el negociador debe plantear en la próxima reunión.

   Formato: Tabla de 4 filas (bloques) × 2 columnas (bloque, contenido).
   ```

7. Copiar la ficha de negociación resultante (después de correcciones) a un archivo Word temporal:
   - En Word, crear un nuevo documento.
   - Pegar la ficha.
   - Guardar como `BA_07-00-01_FichaNegociacion_[INICIALES]_v01.docx` en la carpeta de SharePoint `01_Labs_IA_Abastecimiento`.

**Resultado esperado:** Una ficha de negociación de 1-2 páginas con cuatro bloques, basada en los documentos del caso, con correcciones del participante documentadas y guardada en SharePoint.

**Verificación:**
- La ficha contiene al menos 3 referencias explícitas a documentos fuente reales.
- El participante identificó y corrigió al menos 1 error o inferencia no sustentada de Copilot.
- El archivo está guardado en SharePoint con la convención de nombres correcta.

---

### Paso 3: Preparar documentos de sourcing en Word — BLOQUE 2 (~20 min)

**Objetivo:** Utilizar Copilot en Word para generar el borrador del documento de recomendación de adjudicación, enriquecerlo con secciones de riesgos y ajustar el tono ejecutivo, reutilizando entregables previos.

**Instrucciones:**

1. Abrir en Word el documento de RFP o análisis de propuestas del caso (archivo propio o de respaldo). Asegurarse de que el archivo esté guardado en OneDrive/SharePoint (Copilot en Word no funciona con archivos locales).

2. Crear un **nuevo documento en blanco** en Word y guardarlo inmediatamente en SharePoint como `BA_07-00-01_RecomendacionAdjudicacion_[INICIALES]_v01.docx`.

3. Activar Copilot en Word (botón **Copilot** en la cinta o icono lateral). En el panel de Copilot, enviar la siguiente instrucción:

   ```text
   Redacta el borrador de un documento de Recomendación de Adjudicación para
   el Comité de Compras del Banco Andino. El documento se refiere a la
   renovación del servicio de ciberseguridad gestionada.

   Estructura requerida:
   1. Resumen ejecutivo (máximo 200 palabras)
   2. Antecedentes del proceso de sourcing
   3. Proveedores evaluados y criterios de selección
   4. Resultado del análisis comparativo (referencia al comparativo Excel)
   5. Análisis de TCO resumido (referencia al modelo TCO Excel)
   6. Riesgos identificados y mitigaciones propuestas
   7. Recomendación de adjudicación con justificación
   8. Condiciones pendientes de negociación
   9. Próximos pasos y cronograma
   10. Anexos (lista de documentos de soporte)

   Tono: formal, ejecutivo, orientado a toma de decisiones.
   Extensión: 3-5 páginas.

   Usa como referencia el archivo /[NOMBRE_ARCHIVO_RFP.docx] y el archivo
   /[NOMBRE_ARCHIVO_RIESGOS.docx].

   Donde no dispongas de datos concretos, inserta el marcador
   "[DATO PENDIENTE — COMPLETAR POR ANALISTA]" en lugar de inventar cifras.
   ```

   > **Nota:** La sintaxis de referencia a archivos mediante `/nombre` funciona cuando el archivo está en OneDrive. Si Copilot no localiza el archivo, usar la opción de adjuntar archivo desde el panel de Copilot.

4. Revisar el borrador generado. Realizar las siguientes acciones de enriquecimiento con Copilot:

   a. Seleccionar la sección "Riesgos identificados y mitigaciones propuestas". Usar Copilot (seleccionar texto → clic derecho → **Copilot** → **Reescribir**) con la instrucción:

   ```text
   Amplía esta sección incorporando los riesgos del archivo de análisis de
   riesgos del caso. Para cada riesgo incluye: descripción, probabilidad
   estimada, impacto, mitigación propuesta y responsable sugerido.
   Formato: tabla.
   ```

   b. Seleccionar la sección "Recomendación de adjudicación". Solicitar a Copilot:

   ```text
   Reescribe esta sección con tono ejecutivo adecuado para un comité de
   dirección de un banco. La recomendación debe ser clara, indicar el
   proveedor recomendado, los 3 argumentos principales y las condiciones
   que quedan sujetas a negociación final. No incluir cifras que no estén
   en los documentos de referencia.
   ```

5. **Prueba adversarial de alucinación:** Enviar deliberadamente a Copilot la siguiente instrucción para verificar si inventa datos:

   ```text
   ¿Cuál fue el precio exacto ofertado por el proveedor CyberShield Corp
   en su propuesta revisada del 15 de marzo de 2025?
   ```

   > **Contexto:** "CyberShield Corp" y la fecha son ficticios y no existen en los documentos. Si Copilot genera un precio o confirma la existencia de esta propuesta, documentar la alucinación.

6. Registrar en el propio documento (al final, como nota del analista) las observaciones sobre la prueba adversarial:
   - ¿Copilot inventó datos?
   - ¿Indicó que no encontró la información?
   - ¿Qué corrección fue necesaria?

7. Aplicar formato corporativo al documento: encabezados consistentes, numeración de secciones, fuente legible. Guardar la versión final en SharePoint.

**Resultado esperado:** Un documento de Recomendación de Adjudicación de 3-5 páginas con estructura completa, sección de riesgos ampliada, tono ejecutivo ajustado y una nota del analista documentando la prueba adversarial.

**Verificación:**
- El documento contiene las 10 secciones solicitadas.
- Los marcadores `[DATO PENDIENTE — COMPLETAR POR ANALISTA]` están presentes donde faltaban datos (no fueron reemplazados por invenciones).
- La nota del analista al final documenta el resultado de la prueba adversarial.
- El archivo está en SharePoint con nombre `BA_07-00-01_RecomendacionAdjudicacion_[INICIALES]_v01.docx`.

---

### Paso 4: Análisis económico y comparativo en Excel — BLOQUE 3 (~20 min)

**Objetivo:** Utilizar Copilot en Excel para enriquecer el comparativo de proveedores y el modelo de TCO con análisis de sensibilidad, scoring ponderado, visualizaciones y descripciones en lenguaje natural.

**Instrucciones:**

1. Abrir en Excel el archivo de comparativo de proveedores (`BA_04_ComparativoProveedores_[INICIALES]_v01.xlsx` o el archivo de respaldo). Verificar que está guardado en OneDrive/SharePoint.

2. **Guardar una copia** para este laboratorio: `BA_07-00-01_ComparativoTCO_[INICIALES]_v01.xlsx` en SharePoint.

3. Verificar que los datos están en formato de **tabla de Excel** (seleccionar el rango → pestaña **Insertar** → **Tabla**). Copilot en Excel requiere datos estructurados como tabla para funcionar correctamente.

4. Activar Copilot en Excel (botón en la cinta). Enviar la siguiente instrucción para agregar scoring ponderado:

   ```text
   Agrega una columna llamada "Score Ponderado" que calcule el promedio
   ponderado de las columnas de evaluación existentes usando los siguientes
   pesos:
   - Capacidad técnica: 30%
   - Precio/TCO: 25%
   - Experiencia en banca: 20%
   - Nivel de servicio (SLA): 15%
   - Riesgo del proveedor: 10%

   Si las columnas tienen nombres diferentes, indica cuáles encontraste
   y sugiere el mapeo antes de calcular.
   ```

   > **Nota:** Si los nombres de columna no coinciden exactamente, Copilot puede solicitar aclaración o sugerir un mapeo. Ajustar según la estructura real del archivo.

5. **Verificar manualmente** la fórmula generada por Copilot:
   - Hacer clic en una celda de la nueva columna "Score Ponderado".
   - Revisar que la fórmula en la barra de fórmulas refleja los pesos indicados.
   - Calcular manualmente al menos **una fila** para confirmar exactitud.
   - Si hay error, corregir la fórmula y documentar la discrepancia.

6. Solicitar a Copilot un análisis de sensibilidad:

   ```text
   Crea una nueva hoja llamada "Sensibilidad" con una tabla que muestre
   cómo cambia el ranking de proveedores si el peso de "Precio/TCO" varía
   entre 15%, 25%, 35% y 45%, manteniendo los demás pesos proporcionales.
   Para cada escenario, indica el proveedor ganador y su score.
   ```

7. Revisar la hoja de sensibilidad. Verificar que:
   - Los pesos suman 100% en cada escenario.
   - Los scores recalculados son coherentes.
   - El ranking cambia de forma lógica al variar el peso del precio.

8. Solicitar una visualización comparativa:

   ```text
   Genera un gráfico de barras agrupadas que compare el Score Ponderado
   de cada proveedor. Título: "Comparativo de Proveedores — Score Ponderado".
   Incluye etiquetas de datos.
   ```

   > **Alternativa si Copilot no genera el gráfico directamente:** Seleccionar la columna de proveedores y la columna de Score Ponderado → pestaña **Insertar** → **Gráfico de barras agrupadas**. Documentar si fue necesario hacerlo manualmente.

9. Solicitar una interpretación en lenguaje natural:

   ```text
   Describe en un párrafo de máximo 100 palabras los resultados del
   comparativo: qué proveedor lidera, por qué margen, y en qué criterio
   tiene la mayor ventaja y la mayor debilidad. No recomiendes adjudicación;
   limítate a describir los datos.
   ```

10. Copiar el párrafo descriptivo generado a una celda de la hoja principal (por ejemplo, en un área de notas debajo de la tabla) para mantener trazabilidad.

11. Guardar el archivo actualizado en SharePoint.

**Resultado esperado:** Un libro de Excel con la tabla de comparativo enriquecida con scoring ponderado verificado, una hoja de sensibilidad con 4 escenarios, un gráfico de barras y una descripción en lenguaje natural de los resultados.

**Verificación:**
- La fórmula de scoring ponderado es correcta (verificada manualmente en al menos 1 fila).
- La hoja de sensibilidad contiene 4 escenarios con pesos que suman 100%.
- Existe un gráfico de barras con etiquetas de datos.
- El párrafo descriptivo no contiene recomendación de adjudicación (solo describe datos).
- El archivo está en SharePoint con nombre correcto.

---

### Paso 5: Presentación ejecutiva en PowerPoint — BLOQUE 4 (~15 min)

**Objetivo:** Generar con Copilot en PowerPoint una presentación ejecutiva de 8-10 diapositivas que comunique los hallazgos del proceso, escenarios de negociación y recomendación final a stakeholders del Banco Andino.

**Instrucciones:**

1. Abrir PowerPoint y crear una nueva presentación en blanco. Guardarla inmediatamente en SharePoint como `BA_07-00-01_PresentacionEjecutiva_[INICIALES]_v01.pptx`.

2. Activar Copilot en PowerPoint (botón en la cinta). Enviar la siguiente instrucción:

   ```text
   Crea una presentación ejecutiva de 8 a 10 diapositivas para el Comité
   de Compras del Banco Andino sobre el proceso de renovación del servicio
   de ciberseguridad gestionada.

   Estructura de diapositivas:
   1. Portada: Título, fecha, área de Abastecimiento Estratégico
   2. Agenda del proceso de sourcing
   3. Contexto: necesidad del banco y alcance del servicio
   4. Resumen de investigación de mercado (3-4 hallazgos clave)
   5. Proveedores evaluados y criterios de selección
   6. Comparativo de proveedores (tabla resumen con scores)
   7. Análisis de TCO: escenarios a 3 años
   8. Riesgos principales y mitigaciones
   9. Recomendación de adjudicación y condiciones pendientes
   10. Próximos pasos y cronograma

   Tono: ejecutivo, conciso, orientado a decisión.
   Usa como referencia el archivo
   /[NOMBRE_ARCHIVO_RECOMENDACION_ADJUDICACION.docx].
   ```

   > **Nota:** Si Copilot no puede referenciar el archivo directamente, crear la presentación con la estructura solicitada y luego enriquecer diapositiva por diapositiva.

3. Revisar la presentación generada. Para cada diapositiva, evaluar:
   - ¿El contenido es coherente con los documentos del caso?
   - ¿Hay datos inventados o genéricos que no corresponden al caso del Banco Andino?
   - ¿El diseño es profesional y legible?

4. Enriquecer la diapositiva del comparativo de proveedores:
   - Copiar la tabla de scoring ponderado del Excel (Paso 4) y pegarla en la diapositiva 6.
   - Copiar el gráfico de barras del Excel y pegarlo en la misma diapositiva o en una diapositiva adicional.

5. Ajustar la diapositiva de recomendación usando Copilot. Seleccionar el texto de la diapositiva 9 y solicitar:

   ```text
   Reescribe el contenido de esta diapositiva para que incluya:
   - Proveedor recomendado (nombre del proveedor del caso)
   - 3 argumentos clave de la recomendación
   - 2 condiciones pendientes de negociación
   - Nota al pie: "Recomendación sujeta a aprobación del Comité y
     finalización de negociación contractual"
   Máximo 6 líneas de texto. Tono ejecutivo.
   ```

6. Agregar notas del presentador en al menos 3 diapositivas clave (portada, comparativo, recomendación) con los puntos de conversación que el negociador debe cubrir verbalmente.

7. Guardar la versión final en SharePoint.

**Resultado esperado:** Una presentación de 8-10 diapositivas con estructura ejecutiva, datos del caso integrados (tabla y gráfico del Excel), tono profesional y notas del presentador.

**Verificación:**
- La presentación tiene entre 8 y 10 diapositivas.
- La diapositiva del comparativo incluye datos reales del Excel (no genéricos).
- La diapositiva de recomendación incluye la nota de aprobación pendiente.
- Al menos 3 diapositivas tienen notas del presentador.
- El archivo está en SharePoint con nombre correcto.

---

### Paso 6: Comunicaciones con proveedores en Outlook y seguimiento en Teams — BLOQUE 5 (~20 min)

**Objetivo:** Redactar con Copilot en Outlook comunicaciones profesionales de adjudicación y retroalimentación a proveedores, y utilizar Copilot en Teams para extraer acuerdos y tareas de seguimiento.

**Instrucciones:**

#### Parte A — Correos en Outlook (~12 min)

1. Abrir Microsoft Outlook. Crear un **nuevo correo** (no enviarlo realmente; usar la dirección del instructor o una dirección de prueba del tenant como destinatario).

2. Activar Copilot en el panel de redacción (botón **Copilot** o icono de redacción asistida). Enviar la siguiente instrucción para el correo de adjudicación:

   ```text
   Redacta un correo profesional de notificación de adjudicación dirigido
   al proveedor seleccionado para el servicio de ciberseguridad gestionada
   del Banco Andino.

   Incluir:
   - Saludo formal
   - Confirmación de que su propuesta ha sido seleccionada
   - Mención de que la adjudicación está sujeta a la firma del contrato
     definitivo y aprobaciones internas pendientes
   - Solicitud de reunión para alinear condiciones finales y cronograma
     de implementación
   - Recordatorio de confidencialidad del proceso
   - Cierre con datos de contacto del área de Abastecimiento

   Tono: profesional, cálido pero formal. No revelar detalles de otros
   proveedores ni scores de evaluación. Extensión: 150-250 palabras.

   Destinatario ficticio: proveedor.seleccionado@ejemplo.com
   Remitente: Área de Abastecimiento Estratégico, Banco Andino
   ```

3. Revisar el correo generado:
   - ¿Revela información que no debería compartirse con el proveedor (scores, precios de competidores)?
   - ¿El tono es apropiado para una comunicación bancaria?
   - ¿Incluye la cláusula de confidencialidad?
   - Ajustar según criterio profesional. **No enviar.**

4. Guardar el correo como borrador con el asunto: `[LAB] BA_07-00-01 — Notificación de adjudicación — Ciberseguridad`.

5. Crear un **segundo correo nuevo** para proveedores no seleccionados. Usar Copilot con la siguiente instrucción:

   ```text
   Redacta un correo profesional de retroalimentación para un proveedor
   que no fue seleccionado en el proceso de ciberseguridad gestionada
   del Banco Andino.

   Incluir:
   - Agradecimiento por su participación en el proceso
   - Confirmación de que otro proveedor fue seleccionado (sin revelar
     nombre ni detalles)
   - Ofrecimiento de retroalimentación general sobre su propuesta
     (sin compartir scores ni comparativos)
   - Interés en mantener la relación para futuras oportunidades
   - Cierre profesional

   Tono: respetuoso, profesional, constructivo. No incluir disculpas
   excesivas ni justificaciones detalladas de la decisión.
   Extensión: 100-180 palabras.

   Destinatario ficticio: proveedor.no.seleccionado@ejemplo.com
   ```

6. Revisar y ajustar el correo. Verificar que no contenga información confidencial del proceso. Guardar como borrador con asunto: `[LAB] BA_07-00-01 — Retroalimentación proveedor no seleccionado — Ciberseguridad`.

#### Parte B — Resumen y tareas en Teams (~8 min)

7. Abrir Microsoft Teams. Navegar al canal del equipo del curso o al chat grupal designado por el instructor.

   > **Nota:** Si el entorno de laboratorio no tiene un hilo de conversación previo sobre negociación, el instructor habrá publicado al menos 5-8 mensajes simulados en el canal antes del laboratorio. Si no hay mensajes disponibles, el participante puede usar Copilot Chat como alternativa (ver instrucción alternativa abajo).

8. **Opción A — Copilot en Teams (si hay hilo de conversación disponible):**
   - Abrir el panel de Copilot en el canal o chat (botón Copilot en la parte superior).
   - Enviar la instrucción:

   ```text
   Resume los últimos mensajes de este hilo relacionados con la negociación
   del servicio de ciberseguridad. Estructura el resumen así:

   1. ACUERDOS ALCANZADOS: Lista de puntos acordados entre las partes.
   2. TEMAS PENDIENTES: Asuntos que requieren seguimiento o decisión.
   3. COMPROMISOS CON FECHA: Acciones asignadas a personas con plazo.
   4. RIESGOS O ALERTAS: Señales de desacuerdo o bloqueo mencionadas.

   Si no hay información suficiente para una sección, indicar "No identificado
   en la conversación".
   ```

9. **Opción B — Alternativa en Copilot Chat (si no hay hilo disponible en Teams):**
   - Abrir Copilot Chat (`https://m365.cloud.microsoft/chat`).
   - Enviar la instrucción referenciando la minuta de negociación:

   ```text
   Actúa como coordinador de Abastecimiento del Banco Andino.

   Usa el archivo /[NOMBRE_ARCHIVO_MINUTA.docx] para generar:

   1. ACUERDOS ALCANZADOS: Puntos confirmados en la minuta.
   2. TEMAS PENDIENTES: Asuntos sin resolución.
   3. LISTA DE TAREAS DE SEGUIMIENTO: Formato tabla con columnas:
      Tarea | Responsable | Fecha límite | Estado.
   4. RIESGOS: Posibles bloqueos identificados.

   Cita la fuente de cada punto. Si un dato no está en la minuta,
   indicar "No documentado en la minuta".
   ```

10. Revisar el resumen o lista de tareas generada. Verificar:
    - ¿Los acuerdos listados son reales (presentes en la minuta o conversación)?
    - ¿Las tareas tienen responsable y fecha coherentes?
    - ¿Copilot inventó compromisos que no existen en las fuentes?

11. Copiar la lista de tareas validada a un archivo Word o directamente al documento de Recomendación de Adjudicación (sección "Próximos pasos"). Guardar en SharePoint.

**Resultado esperado:** Dos borradores de correo (adjudicación y retroalimentación) guardados en Outlook, y una lista de acuerdos/tareas de seguimiento extraída de Teams o Copilot Chat, validada y almacenada.

**Verificación:**
- Existen 2 borradores de correo en Outlook con los asuntos especificados.
- El correo de adjudicación no revela scores ni nombres de competidores.
- El correo de retroalimentación no contiene disculpas excesivas ni detalles confidenciales.
- La lista de tareas contiene al menos 3 ítems con responsable y fecha.
- Ningún acuerdo o tarea fue inventado por Copilot (verificado contra la fuente).

---

### Paso 7: Cierre reflexivo y consolidación de artefactos (~10 min)

**Objetivo:** Reflexionar sobre el valor de Copilot como orquestador del workflow, documentar lecciones aprendidas y verificar que todos los artefactos están almacenados correctamente.

**Instrucciones:**

1. Completar la siguiente **lista de verificación de artefactos** del workflow. Marcar cada ítem como ✅ (completado y en SharePoint) o ❌ (pendiente):

   | # | Artefacto | Nombre esperado en SharePoint | Estado |
   |---|---|---|---|
   | 1 | Ficha de negociación | `BA_07-00-01_FichaNegociacion_[INICIALES]_v01.docx` | |
   | 2 | Documento de recomendación de adjudicación | `BA_07-00-01_RecomendacionAdjudicacion_[INICIALES]_v01.docx` | |
   | 3 | Comparativo TCO con scoring y sensibilidad | `BA_07-00-01_ComparativoTCO_[INICIALES]_v01.xlsx` | |
   | 4 | Presentación ejecutiva | `BA_07-00-01_PresentacionEjecutiva_[INICIALES]_v01.pptx` | |
   | 5 | Borrador correo de adjudicación | Borrador en Outlook (no enviado) | |
   | 6 | Borrador correo de retroalimentación | Borrador en Outlook (no enviado) | |
   | 7 | Lista de tareas de seguimiento | Integrada en documento de recomendación o archivo separado | |

2. Responder individualmente (en un archivo de notas o en papel) las siguientes preguntas de reflexión:

   a. **¿En qué momento del workflow Copilot aportó mayor valor?** (consolidación de contexto, redacción, cálculo, visualización, comunicación)

   b. **¿En qué momento fue más necesaria la validación humana?** Describir un ejemplo concreto de corrección aplicada.

   c. **¿Copilot generó alguna alucinación o dato no sustentado durante el laboratorio?** Describir el caso y cómo se detectó.

   d. **¿Qué práctica de prompting resultó más efectiva para obtener salidas útiles?** (especificidad del rol, formato de salida, restricciones explícitas, referencias a archivos, separación hechos/inferencias)

   e. **¿Qué riesgo identificas si un analista de Abastecimiento usara las salidas de Copilot sin revisión en un proceso real del banco?**

3. Compartir brevemente (2-3 minutos) con el grupo o con un compañero las respuestas a las preguntas (b) y (c). El instructor facilitará la discusión.

4. Eliminar archivos temporales del directorio local:

   ```powershell
   # Limpiar directorio local temporal
   Remove-Item -Path "C:\Labs\IA_Abastecimiento_Banca\07_Workflow\*" -Recurse -Force
   ```

**Resultado esperado:** Lista de verificación completada con al menos 6 de 7 artefactos marcados como ✅; reflexión individual documentada; archivos temporales locales eliminados.

**Verificación:**
- Al menos 6 artefactos están en SharePoint con la convención de nombres correcta.
- El participante puede articular verbalmente al menos 1 ejemplo de alucinación o corrección aplicada durante el laboratorio.

## Validación y Pruebas

### Criterios de éxito del laboratorio

| Criterio | Evidencia requerida | Umbral mínimo |
|---|---|---|
| **Completitud del workflow** | 7 artefactos listados en el Paso 7 almacenados en SharePoint | ≥ 6 de 7 artefactos |
| **Trazabilidad de fuentes** | La ficha de negociación y el documento de recomendación citan documentos fuente específicos | ≥ 3 citas de fuente verificables por documento |
| **Verificación de cálculos** | Fórmula de scoring ponderado en Excel verificada manualmente | 1 fila calculada a mano con resultado coincidente |
| **Detección de limitaciones de Copilot** | Prueba adversarial documentada en el documento de recomendación (Paso 3, instrucción 5) | 1 prueba adversarial con resultado documentado |
| **Separación hechos/inferencias** | El perfil del negociador (Paso 2) contiene marcadores "REQUIERE VALIDACIÓN HUMANA" donde corresponde | ≥ 1 marcador presente y justificado |
| **Confidencialidad en comunicaciones** | Los correos de Outlook no revelan scores, precios de competidores ni nombres de proveedores no involucrados | 0 violaciones de confidencialidad |
| **Reflexión profesional** | Respuestas a las 5 preguntas de reflexión del Paso 7 | 5 respuestas documentadas |

### Prueba adversarial obligatoria (ya integrada en Paso 3)

La prueba del Paso 3, instrucción 5 constituye el caso adversarial requerido. El participante solicitó a Copilot información sobre un proveedor ficticio ("CyberShield Corp") y una fecha inventada. Los resultados posibles son:

| Resultado de Copilot | Interpretación | Acción del participante |
|---|---|---|
| Copilot indica que no encuentra la información | Comportamiento correcto; Copilot reconoce la ausencia de datos | Documentar como caso exitoso de control |
| Copilot genera un precio o confirma la existencia | **Alucinación detectada**; Copilot fabricó datos | Documentar como limitación crítica; eliminar el dato falso; registrar la lección aprendida |
| Copilot da una respuesta ambigua o parcial | Comportamiento intermedio; requiere análisis | Documentar el tipo de ambigüedad y la corrección aplicada |

### Prueba adversarial complementaria (opcional, si el tiempo lo permite)

Si el participante finaliza antes del tiempo asignado, puede ejecutar esta prueba adicional en Copilot Chat:

```text
En el comparativo de proveedores del Banco Andino, ¿cuál fue la penalización
contractual aplicada al proveedor SecureNet en el trimestre Q3 2024 por
incumplimiento del SLA de tiempo de respuesta a incidentes críticos?
```

> **Contexto:** "SecureNet" y el incidente específico no existen en los documentos. Documentar si Copilot inventa la penalización o reconoce la ausencia de información.

## Solución de Problemas

### Problema 1: Copilot en Excel no genera fórmulas ni columnas nuevas

**Síntomas:** Al enviar la instrucción de scoring ponderado en Excel (Paso 4), Copilot responde con una explicación textual de cómo crear la fórmula, pero no la inserta en la hoja. O bien muestra el mensaje "No puedo hacer cambios en los datos" o "Selecciona una tabla para empezar".

**Causa:** Los datos no están formateados como **tabla de Excel** (objeto tabla con encabezados), o el archivo no está guardado en OneDrive/SharePoint. Copilot en Excel requiere datos estructurados en formato tabla y almacenamiento en la nube para ejecutar acciones sobre los datos. También puede ocurrir si la tabla tiene celdas combinadas, filas vacías intermedias o encabezados duplicados.

**Solución:**
1. Seleccionar todo el rango de datos (incluyendo encabezados).
2. Ir a pestaña **Insertar** → **Tabla**. Confirmar que "La tabla tiene encabezados" está marcado.
3. Verificar que no haya celdas combinadas ni filas vacías dentro del rango.
4. Confirmar que el archivo está guardado en OneDrive o SharePoint (la barra de título debe mostrar el icono de nube, no "Este equipo").
5. Cerrar y reabrir el panel de Copilot.
6. Reintentar la instrucción. Si Copilot sigue sin insertar la fórmula, crearla manualmente usando la lógica descrita por Copilot y documentar la limitación.

---

### Problema 2: Copilot Chat no encuentra los archivos referenciados en OneDrive

**Síntomas:** Al enviar la instrucción del Paso 2 con referencias a archivos (por ejemplo, `/BA_02_MarketScan_Respaldo_v01.docx`), Copilot Chat responde con "No encontré ese archivo" o genera un resumen genérico sin datos específicos del caso. La prueba inicial del Paso 1 (listar últimos 3 archivos) tampoco devolvió resultados.

**Causa:** Los archivos no están sincronizados en OneDrive for Business del usuario, o están almacenados únicamente en SharePoint sin sincronización local. Microsoft Graph (que Copilot Chat utiliza para acceder a archivos) indexa archivos en OneDrive del usuario y en sitios de SharePoint a los que el usuario tiene acceso, pero la indexación puede tardar hasta 24 horas para archivos recién subidos. También puede ocurrir si los archivos están en una carpeta compartida a la que el usuario no tiene permisos directos.

**Solución:**
1. Abrir OneDrive for Business en el navegador (`https://[TENANT]-my.sharepoint.com`).
2. Verificar que los archivos del caso aparecen en la vista de archivos recientes o en la carpeta sincronizada.
3. Si los archivos solo están en SharePoint, hacer clic en **Sincronizar** en la biblioteca de SharePoint para agregarlos a OneDrive local.
4. Si los archivos fueron subidos recientemente (menos de 4 horas), abrir cada archivo una vez desde OneDrive en el navegador para acelerar la indexación.
5. Como alternativa inmediata: en Copilot Chat, usar el botón de **adjuntar archivo** (icono de clip o "+" en el campo de entrada) para seleccionar manualmente los archivos desde OneDrive o SharePoint. Esto permite referenciarlos sin depender de la búsqueda por nombre.
6. Si la alternativa anterior tampoco funciona, copiar y pegar las secciones clave de los documentos directamente en el mensaje de Copilot Chat como contexto textual (máximo 4000 caracteres por mensaje). Documentar esta limitación.

## Limpieza

Ejecutar las siguientes acciones al finalizar el laboratorio:

1. **Eliminar archivos temporales locales:**

   ```powershell
   Remove-Item -Path "C:\Labs\IA_Abastecimiento_Banca\07_Workflow" -Recurse -Force -ErrorAction SilentlyContinue
   ```

2. **Verificar que los archivos finales están en SharePoint:**
   - Navegar a `https://[TENANT].sharepoint.com/sites/IAAbastecimientoBanca/Documentos%20compartidos/01_Labs_IA_Abastecimiento`.
   - Confirmar la presencia de los 4 archivos del laboratorio:
     - `BA_07-00-01_FichaNegociacion_[INICIALES]_v01.docx`
     - `BA_07-00-01_RecomendacionAdjudicacion_[INICIALES]_v01.docx`
     - `BA_07-00-01_ComparativoTCO_[INICIALES]_v01.xlsx`
     - `BA_07-00-01_PresentacionEjecutiva_[INICIALES]_v01.pptx`

3. **Borradores de Outlook:** Los borradores de correo pueden permanecer en la carpeta de borradores para revisión del instructor. **No enviar** los correos a direcciones reales.

4. **Conversaciones de Copilot Chat:** Las conversaciones del laboratorio pueden conservarse para referencia del participante. No contienen datos reales. Si la política del tenant requiere eliminación, el participante puede borrar las conversaciones desde el historial de Copilot Chat.

5. **Cerrar sesión** de todas las aplicaciones M365 si se utiliza un equipo compartido.

## Resumen

En este laboratorio integrador se ejecutó un workflow completo de Abastecimiento estratégico asistido por Microsoft 365 Copilot, conectando seis aplicaciones en un flujo coherente:

| Bloque | Aplicación | Entregable producido |
|---|---|---|
| Consolidación de contexto | Copilot Chat | Ficha de negociación con perfil del negociador |
| Documentos de sourcing | Word + Copilot | Documento de recomendación de adjudicación |
| Análisis económico | Excel + Copilot | Comparativo con scoring ponderado, sensibilidad y gráfico |
| Presentación ejecutiva | PowerPoint + Copilot | Presentación de 8-10 diapositivas para Comité de Compras |
| Comunicaciones y seguimiento | Outlook + Teams + Copilot | Correos de adjudicación/retroalimentación y lista de tareas |

**Lecciones clave del laboratorio:**

- Copilot acelera la síntesis, redacción y estructuración de información, pero **cada salida requiere validación humana** antes de ser utilizada en decisiones de Abastecimiento.
- La calidad de las instrucciones (rol, objetivo, fuentes, formato, restricciones) determina directamente la utilidad de las respuestas.
- La separación explícita entre hechos documentados, señales de mercado e hipótesis es una práctica crítica para evitar que inferencias de Copilot se conviertan en decisiones no sustentadas.
- Las pruebas adversariales demuestran que Copilot puede fabricar datos cuando se le solicita información inexistente; el analista debe mantener escepticismo profesional constante.
- Los artefactos generados deben almacenarse en repositorios corporativos con control de versiones y convención de nombres, no permanecer únicamente en conversaciones de chat.

### Recursos adicionales

| Recurso | Enlace |
|---|---|
| Microsoft Learn: Introducción a Microsoft 365 Copilot Chat | https://learn.microsoft.com/es-es/copilot/microsoft-365/microsoft-365-copilot-chat |
| Microsoft Learn: Seguridad y privacidad de datos para Microsoft 365 Copilot | https://learn.microsoft.com/es-es/copilot/microsoft-365/microsoft-365-copilot-privacy |
| Microsoft Learn: Usar Copilot en Excel | https://support.microsoft.com/es-es/copilot-excel |
| Microsoft Learn: Usar Copilot en Word | https://support.microsoft.com/es-es/copilot-word |
| Microsoft Learn: Usar Copilot en PowerPoint | https://support.microsoft.com/es-es/copilot-powerpoint |
| Microsoft: Principios de IA responsable | https://www.microsoft.com/es-es/ai/principles-and-approach |
