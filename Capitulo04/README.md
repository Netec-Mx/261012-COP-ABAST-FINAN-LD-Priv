# Práctica: Construir y analizar un TCO y business case con Copilot en Excel

## Metadatos

| Atributo | Valor |
|---|---|
| **Duración** | 105 minutos |
| **Complejidad** | Alta |
| **Nivel Bloom** | Aplicar |
| **Herramienta principal** | Microsoft 365 Copilot en Excel (servicio SaaS, licencia Copilot Add-on para Microsoft 365 E3/E5) |
| **Aplicación host** | Microsoft Excel – Microsoft 365 Apps for Enterprise, versión 2405 (Build 17628.20164) |
| **Almacenamiento** | OneDrive for Business (servicio SaaS administrado por Microsoft) |
| **Colaboración** | Microsoft Teams, versión 24124.1412.2911.4561 |
| **Sistema operativo** | Windows 11 Pro 23H2 (Build 22631.4169) |

## Descripción General

En este laboratorio construirás un modelo de Costo Total de Propiedad (TCO) y business case para tres casos de abastecimiento del Banco Andino — biometría, consumo de IA y Contact Center — utilizando Microsoft 365 Copilot en Excel como asistente de modelación. Partirás de datos crudos de laboratorio, los limpiarás y normalizarás con apoyo de Copilot, estructurarás inputs de TCO a 5 años, calcularás métricas financieras (VPN, TIR, payback), ejecutarás análisis de escenarios y sensibilidad, documentarás supuestos con trazabilidad y producirás un resumen ejecutivo. Cada fórmula y resultado generado por Copilot será validado por ti antes de aceptarse, reforzando el principio de supervisión humana obligatoria.

## Objetivos de Aprendizaje

Al completar este laboratorio serás capaz de:

- [ ] Organizar y limpiar un dataset de Spend de tres casos bancarios (biometría, IA, Contact Center) utilizando prompts dirigidos a Copilot en Excel para identificar inconsistencias, normalizar unidades y generar columnas calculadas.
- [ ] Estructurar un modelo de TCO a 5 años con categorías CAPEX, OPEX, costos de integración, escalación y salida, solicitando a Copilot la generación de fórmulas y validando la lógica financiera resultante.
- [ ] Calcular VPN (tasa 12%), TIR y período de payback para comparar alternativas de abastecimiento, verificando referencias de celda, unidades y coherencia económica de cada fórmula generada por Copilot.
- [ ] Construir escenarios comparativos (optimista y conservador) y ejecutar análisis de sensibilidad sobre variables críticas, utilizando Copilot para crear tablas de datos y para identificar puntos de quiebre entre alternativas.
- [ ] Documentar supuestos, fuentes y trazabilidad en una hoja dedicada y comunicar resultados en un resumen ejecutivo estructurado, diferenciando datos confirmados, estimaciones y beneficios no validados.

## Prerrequisitos

### Conocimientos requeridos

| Área | Detalle |
|---|---|
| Copilot en Microsoft 365 | Haber completado los laboratorios de los Módulos 1, 2 y 3 del curso, o experiencia equivalente con prompts en Copilot Chat y Copilot en aplicaciones de Microsoft 365. |
| Excel intermedio | Fórmulas: `SUMA`, `PROMEDIO`, `SI`, `BUSCARX`/`BUSCARV`. Creación de tablas (`Ctrl+T`), referencias entre hojas, formato condicional. |
| Conceptos financieros básicos | TCO, VPN (Valor Presente Neto), TIR (Tasa Interna de Retorno), payback period. No se requiere formación avanzada en finanzas corporativas. |
| Casos del curso | Familiaridad con los tres escenarios de abastecimiento del Banco Andino: biometría (30M–40M clientes), consumo de IA (70B–100B tokens/año) y Contact Center (300M llamadas/año). |

### Acceso y licencias requeridos

| Recurso | Requisito |
|---|---|
| Cuenta Microsoft Entra ID | Habilitada en el tenant de capacitación con acceso a OneDrive for Business. |
| Licencia Microsoft 365 Copilot | Copilot Add-on activo y verificado. El botón Copilot debe aparecer habilitado (no en gris) en la pestaña **Inicio** de Excel al abrir un archivo desde OneDrive. |
| Archivo de datos base | `Lab_TCO_Datos_Base.xlsx` distribuido por el instructor vía Teams y guardado en `OneDrive/Documentos/Lab_TCO_Copilot/`. |
| Conexión a Internet | Mínimo 20 Mbps descarga / 5 Mbps carga, con acceso HTTPS a dominios de Microsoft 365. |

## Entorno de Laboratorio

### Hardware mínimo

| Componente | Especificación |
|---|---|
| Procesador | 64 bits, 4 núcleos o superior |
| RAM | 16 GB recomendados (8 GB mínimo) |
| Almacenamiento libre | 10 GB para sincronización de OneDrive y archivos temporales |
| Pantalla | 1920 × 1080 mínimo; se recomienda monitor adicional |

### Software requerido

| Software | Versión exacta | Fuente oficial |
|---|---|---|
| Windows 11 Pro | 23H2, Build 22631.4169 | [Página de descarga Windows 11](https://www.microsoft.com/es-es/windows/windows-11) |
| Microsoft Excel (Microsoft 365 Apps for Enterprise) | Versión 2405, Build 17628.20164 | [Portal de instalación Microsoft 365](https://portal.office.com/account#installs) |
| Microsoft Edge | 128.0.2739.79 | [Descarga Edge](https://www.microsoft.com/es-es/edge) |
| Microsoft Teams | 24124.1412.2911.4561 | Cliente administrado por el tenant |
| Microsoft 365 Copilot en Excel | Servicio SaaS (sin versión fija publicable) | [Documentación Copilot en Excel](https://support.microsoft.com/es-es/topic/bienvenido-a-copilot-en-excel-3a92b0c2-0b8d-4d8e-bc20-90b0db9c12f7) |
| OneDrive for Business | Servicio SaaS administrado por Microsoft | [Documentación OneDrive](https://support.microsoft.com/es-es/onedrive) |

### Preparación del entorno

1. Abre Microsoft Teams y descarga el archivo `Lab_TCO_Datos_Base.xlsx` que el instructor compartirá en el canal del curso.
2. Guarda el archivo en la ruta: **OneDrive > Documentos > Lab_TCO_Copilot**.
3. Abre el archivo desde OneDrive (no desde una copia local) haciendo doble clic en el Explorador de archivos o desde la interfaz web de OneDrive.
4. Verifica que el ícono de **Copilot** en la pestaña **Inicio** de Excel aparece en color (activo). Si aparece en gris, cierra el archivo, espera 30 segundos para que OneDrive complete la sincronización y vuelve a abrirlo.
5. Crea el directorio local temporal `C:\Labs\IA_Abastecimiento_Banca\Lab04\` para capturas de pantalla y notas de trabajo.

### Estructura del archivo de datos base

El archivo `Lab_TCO_Datos_Base.xlsx` contiene las siguientes hojas prellenadas con datos sintéticos del Banco Andino:

| Hoja | Contenido | Registros aproximados |
|---|---|---|
| `Biometria_Raw` | Volúmenes de clientes (30M–40M), transacciones (referencia 1B), tarifas por proveedor, costos de integración | 35 filas |
| `IA_Tokens_Raw` | Consumo de tokens por año (70B–100B), tarifas por millón de tokens, opciones de 3 proveedores | 30 filas |
| `ContactCenter_Raw` | Volumen de llamadas (300M/año), costos de agentes, IPC 6%, aumento SMMLV 23%, tarifas de plataforma | 40 filas |
| `Parametros_Lab` | Tasa de descuento (12%), horizonte (5 años), moneda (COP), inflación, factores de escalación | 15 filas |

> **Nota sobre datos sintéticos:** Todos los valores son ficticios y diseñados para el laboratorio. Cuando falten tarifas reales, se utilizarán los valores de laboratorio provistos en `Parametros_Lab` para poder comparar alternativas y construir el TCO. Está prohibido cargar datos reales de proveedores, contratos o información bancaria.

### Convención de nombres para archivos generados

Todos los archivos finales deben seguir el formato:

```
BA_04-00-01_[Artefacto]_[InicialesParticipante]_v01.xlsx
```

Ejemplo: `BA_04-00-01_TCO_BusinessCase_JP_v01.xlsx`

## Instrucciones Paso a Paso

---

### Paso 1: Organización y limpieza de datos de Spend (15 min)

**Objetivo:** Identificar inconsistencias en los datos crudos de los tres casos y generar columnas normalizadas utilizando Copilot en Excel, validando cada transformación antes de aplicarla.

**Instrucciones:**

1. Abre el archivo `Lab_TCO_Datos_Base.xlsx` desde OneDrive. Confirma que aparece la etiqueta **"Guardado automáticamente"** en la barra de título.

2. Navega a la hoja `Biometria_Raw`. Selecciona todo el rango de datos y conviértelo en tabla de Excel:
   - Selecciona cualquier celda con datos → **Insertar > Tabla** (o `Ctrl+T`).
   - Marca la casilla **"La tabla tiene encabezados"**.
   - Renombra la tabla como `tbl_Biometria_Raw` en la pestaña **Diseño de tabla > Nombre de la tabla**.

3. Repite el paso anterior para las hojas `IA_Tokens_Raw` (tabla: `tbl_IA_Raw`) y `ContactCenter_Raw` (tabla: `tbl_CC_Raw`).

4. Regresa a la hoja `Biometria_Raw`. Abre el panel de Copilot haciendo clic en el botón **Copilot** de la pestaña **Inicio**. Escribe el siguiente prompt:

   > Analiza la tabla `tbl_Biometria_Raw`. Identifica: (1) valores nulos o vacíos en columnas numéricas, (2) inconsistencias en unidades — por ejemplo, si algunos valores están en millones y otros en unidades absolutas, (3) proveedores que podrían ser duplicados con nombres ligeramente diferentes. Lista los problemas encontrados sin modificar los datos.

5. Revisa la respuesta de Copilot. Anota en una celda de comentario o en un archivo de notas local (`C:\Labs\IA_Abastecimiento_Banca\Lab04\notas_limpieza.txt`) cuáles problemas identificó correctamente y cuáles omitió o describió incorrectamente. **No aceptes la respuesta sin verificación.**

6. Solicita a Copilot la creación de una columna normalizada de volumen. Usa el siguiente prompt:

   > Agrega una columna calculada llamada "Volumen_Normalizado_M" que convierta todos los valores de volumen de clientes a millones. Si el valor original ya está en millones, cópialo directamente. Si está en unidades absolutas (valores mayores a 1.000.000), divídelo entre 1.000.000. Muestra la fórmula que usarás antes de aplicarla.

7. Examina la fórmula propuesta por Copilot. Verifica que:
   - La referencia de columna es correcta.
   - La lógica condicional (`SI`) distingue correctamente entre unidades.
   - No hay errores de referencia circular.
   Si la fórmula es correcta, acepta la inserción. Si no, corrige manualmente y documenta la corrección.

8. Repite el proceso de limpieza para `IA_Tokens_Raw` con este prompt:

   > Analiza la tabla `tbl_IA_Raw`. Estandariza el consumo de tokens a "billones de tokens/año" (1 billón = 1.000.000.000.000 en escala larga hispanoamericana, equivalente a 1 trillion en escala corta anglosajona). Crea una columna "Tokens_Billones_Año" con la conversión. Identifica si hay proveedores con nombres duplicados o tarifas que parezcan atípicas respecto al rango de los demás.

9. Para `ContactCenter_Raw`, solicita:

   > Analiza la tabla `tbl_CC_Raw`. Verifica que el volumen de llamadas esté expresado en millones/año de forma consistente. Identifica si los costos de mano de obra incluyen o excluyen cargas sociales y si hay filas donde el IPC o el factor SMMLV no estén aplicados. No modifiques datos; solo reporta inconsistencias.

10. Guarda el archivo (`Ctrl+S`). Verifica que la sincronización con OneDrive se complete (ícono de nube con check verde).

**Resultado esperado:**

- Tres tablas de Excel nombradas (`tbl_Biometria_Raw`, `tbl_IA_Raw`, `tbl_CC_Raw`) con encabezados claros.
- Al menos una columna normalizada por tabla (volumen en millones, tokens en billones, llamadas en millones).
- Un registro de las inconsistencias detectadas por Copilot y las validadas/corregidas por el participante.

**Verificación:**

- [ ] Cada hoja tiene datos en formato de tabla de Excel (aparece la pestaña **Diseño de tabla** al seleccionar una celda).
- [ ] Las columnas normalizadas no contienen errores `#REF!`, `#VALOR!` o `#N/A`.
- [ ] Se documentó al menos un caso donde Copilot identificó correctamente un problema y al menos un caso donde su respuesta fue incompleta o imprecisa.

---

### Paso 2: Estructuración de inputs para TCO a 5 años (20 min)

**Objetivo:** Construir la hoja `TCO_Inputs` con categorías de costos (CAPEX, OPEX, integración, soporte, escalación, salida) para los tres casos, utilizando Copilot para proponer la estructura y fórmulas de referencia cruzada.

**Instrucciones:**

1. Crea una nueva hoja en el libro y nómbrala `TCO_Inputs`.

2. Abre el panel de Copilot y solicita la estructura base con el siguiente prompt:

   > Soy analista de Abastecimiento del Banco Andino. Necesito estructurar los inputs de un modelo de TCO a 5 años para comparar alternativas de tres categorías de compra: (1) plataforma de biometría con crecimiento de 30 a 40 millones de clientes, (2) consumo de IA de 70 a 100 billones de tokens/año, y (3) Contact Center con 300 millones de llamadas/año. Propón una estructura de tabla con estas columnas: Caso, Alternativa, Categoría de Costo (CAPEX inicial, OPEX recurrente, Integración, Soporte, Escalación por volumen, Transición/Salida), Año 0, Año 1, Año 2, Año 3, Año 4, Año 5, Fuente del dato, Tipo (Confirmado / Estimado / Supuesto de laboratorio). No inventes valores numéricos; solo genera la estructura vacía con las filas necesarias para al menos 2 alternativas por caso.

3. Revisa la estructura propuesta. Copilot puede generar la tabla directamente o describir la estructura en texto. Si genera una tabla, verifícala y ajusta según necesites. Si solo describe, crea manualmente la estructura siguiendo la propuesta.

4. Convierte el rango en tabla de Excel: `Ctrl+T`, nombre: `tbl_TCO_Inputs`.

5. Ahora completa los valores numéricos usando los datos de las hojas de origen. Solicita a Copilot fórmulas de referencia cruzada:

   > Crea una fórmula que traiga el valor de la tarifa por transacción biométrica del proveedor A desde la tabla `tbl_Biometria_Raw` a la fila correspondiente de `tbl_TCO_Inputs`. Usa BUSCARX o INDICE/COINCIDIR. Muéstrame la fórmula antes de insertarla.

6. Verifica la fórmula propuesta. Confirma que:
   - La referencia a la hoja de origen es correcta (nombre de tabla, columna).
   - El criterio de búsqueda coincide exactamente con los valores de la tabla de origen.
   - El resultado tiene las unidades esperadas (COP, USD, etc.).

7. Para las filas donde no existan tarifas reales, utiliza los valores de laboratorio de la hoja `Parametros_Lab`. Inserta manualmente o con fórmula de referencia, y marca la columna **Tipo** como `Supuesto de laboratorio`.

8. Para el caso de **Contact Center**, crea las filas de costo de mano de obra con escalación. Solicita a Copilot:

   > Para el caso de Contact Center, necesito calcular el costo de mano de obra de agentes para cada año del modelo TCO (Año 1 a Año 5). El costo base en Año 1 es el valor de la hoja `tbl_CC_Raw`. A partir del Año 2, el costo se incrementa anualmente por dos factores: IPC del 6% y aumento del SMMLV del 23%. Estos factores no se suman directamente; el IPC aplica al componente de costos operativos generales y el SMMLV aplica al componente salarial de agentes. Propón una fórmula que separe ambos componentes y los escale año a año. Usa celdas de la hoja `Parametros_Lab` para los factores.

9. Revisa críticamente la fórmula. El aumento de SMMLV del 23% es un incremento acumulado para el primer año del modelo (dato de laboratorio); verifica que Copilot no lo aplique como 23% compuesto cada año sin tu confirmación. **Este es un punto donde Copilot puede asumir incorrectamente una tasa compuesta.** Si detectas este error, corrígelo y documenta la corrección.

10. Para el caso de **Biometría**, modela el crecimiento de volumen:

    > Para biometría, el volumen de clientes crece de 30 millones a 40 millones en 5 años. Propón una fórmula que distribuya este crecimiento de forma lineal (2 millones adicionales por año) y calcule el costo variable anual multiplicando el volumen del año por la tarifa por cliente. Referencia la tarifa desde `tbl_Biometria_Raw` y el volumen inicial desde `Parametros_Lab`.

11. Para el caso de **IA**, modela la progresión de consumo:

    > Para consumo de IA, el volumen progresa de 70 billones a 100 billones de tokens/año en 5 años. Propón una distribución del crecimiento y calcula el costo anual multiplicando tokens consumidos por la tarifa por millón de tokens de cada proveedor. Usa los datos de `tbl_IA_Raw` y `Parametros_Lab`.

12. Guarda el archivo (`Ctrl+S`).

**Resultado esperado:**

- Hoja `TCO_Inputs` con tabla `tbl_TCO_Inputs` que contiene al menos 2 alternativas por caso (6 alternativas mínimo), con costos distribuidos en Año 0 a Año 5.
- Fórmulas de referencia cruzada a las hojas de datos de origen.
- Columna **Tipo** completada indicando si cada valor es confirmado, estimado o supuesto de laboratorio.
- Escalación de costos de Contact Center con IPC y SMMLV aplicados correctamente.

**Verificación:**

- [ ] La tabla `tbl_TCO_Inputs` no contiene errores de fórmula.
- [ ] Los costos de Contact Center del Año 5 son significativamente mayores que los del Año 1 debido a la escalación.
- [ ] El volumen de biometría en Año 5 refleja 40M de clientes (no 30M).
- [ ] El consumo de IA en Año 5 refleja 100B tokens/año.
- [ ] Al menos un caso de corrección a Copilot está documentado (por ejemplo, la aplicación incorrecta del factor SMMLV).

---

### Paso 3: Cálculo de TCO y métricas financieras del business case (25 min)

**Objetivo:** Calcular el TCO total a 5 años, VPN (tasa 12%), TIR y payback period para cada alternativa de los tres casos, solicitando fórmulas a Copilot y validando la lógica financiera.

**Instrucciones:**

1. Crea tres nuevas hojas: `TCO_Biometria`, `TCO_IA_Tokens` y `TCO_ContactCenter`.

2. En la hoja `TCO_Biometria`, construye la tabla de resumen de TCO. Solicita a Copilot:

   > Crea una tabla de resumen de TCO para el caso de biometría con la siguiente estructura: filas para cada categoría de costo (CAPEX, OPEX, Integración, Soporte, Escalación, Salida) y columnas para Año 0 a Año 5, Total Nominal y Total VPN. Agrega filas para: Total de costos, Beneficios/Ahorros, Costo Neto, Flujo de caja neto acumulado. Trae los valores desde `tbl_TCO_Inputs` filtrando por el caso "Biometría" y la alternativa correspondiente. Muéstrame las fórmulas antes de insertarlas.

3. Revisa las fórmulas de totalización. Confirma que:
   - `SUMA` abarca las filas correctas (no incluye la fila de total dentro de sí misma).
   - Los beneficios se restan (flujo neto = costos − ahorros, o costos + beneficios con signo negativo).
   - No hay referencias circulares.

4. Solicita la fórmula de VPN (Valor Presente Neto) a Copilot:

   > Calcula el Valor Presente Neto (VPN) del flujo de caja neto de la alternativa A de biometría usando una tasa de descuento del 12% anual. La tasa está en la celda `Parametros_Lab!B3`. Usa la función VNA() de Excel. El Año 0 es el momento presente (no se descuenta). Muéstrame la fórmula completa.

5. **Validación crítica de la fórmula VNA():** La función `VNA()` de Excel descuenta desde el período 1. Si el Año 0 tiene un desembolso, debe sumarse por separado:

   ```excel
   =Año0 + VNA(Parametros_Lab!$B$3, Año1, Año2, Año3, Año4, Año5)
   ```

   Verifica que Copilot aplique esta convención correctamente. Si incluye el Año 0 dentro de `VNA()`, el resultado estará descontando un período de más. **Documenta si Copilot comete este error.**

6. Solicita la fórmula de TIR:

   > Calcula la TIR (Tasa Interna de Retorno) del flujo de caja neto de la alternativa A de biometría usando la función TIR() de Excel. Los flujos van del Año 0 al Año 5. Incluye una estimación inicial del 10%.

   ```excel
   =TIR(rango_flujos, 0.10)
   ```

7. Solicita el cálculo de payback period:

   > Calcula el período de recuperación (payback period) de la alternativa A de biometría. Crea una fila de flujo de caja acumulado y usa una fórmula que identifique en qué año el acumulado pasa de negativo a positivo. Si quieres mayor precisión, interpola linealmente dentro del año de cruce.

8. Revisa la fórmula de payback. Un enfoque válido es:

   ```excel
   =COINCIDIR(1, SI(rango_acumulado>=0, 1), 0)
   ```

   Para interpolación:
   ```excel
   =Año_anterior_al_cruce + ABS(Acumulado_año_anterior) / Flujo_año_de_cruce
   ```

9. Replica la estructura para la **Alternativa B** de biometría en la misma hoja (debajo o al lado).

10. Repite los pasos 2–9 para las hojas `TCO_IA_Tokens` y `TCO_ContactCenter`, adaptando los prompts al caso correspondiente. Para Contact Center, asegúrate de que la escalación por IPC (6%) y SMMLV (23%) se refleje en los costos de cada año.

    Para IA, usa un prompt como:

    > Calcula el TCO a 5 años para la alternativa A de consumo de IA. El volumen crece de 70B a 100B tokens/año. La tarifa es de [valor de tbl_IA_Raw] por millón de tokens. Incluye costos de integración en Año 0, OPEX de plataforma anual y costo variable por consumo. Calcula VPN al 12%, TIR y payback.

11. Crea una tabla comparativa en cada hoja que muestre lado a lado: TCO nominal, TCO descontado (VPN), TIR, payback y ahorro vs. línea base para las dos alternativas.

12. Guarda el archivo (`Ctrl+S`).

**Resultado esperado:**

- Tres hojas de TCO con al menos 2 alternativas cada una.
- Métricas calculadas: TCO nominal a 5 años, VPN al 12%, TIR y payback period.
- Tabla comparativa por caso.
- Fórmulas verificadas y documentación de al menos una corrección a Copilot.

**Verificación:**

- [ ] La función `VNA()` no descuenta el Año 0 (el desembolso inicial se suma por separado).
- [ ] La TIR devuelve un valor numérico (no `#NUM!`); si devuelve error, hay un problema con los signos de los flujos.
- [ ] El payback period es un número entre 0 y 5 para al menos una alternativa de cada caso.
- [ ] Los costos de Contact Center en Año 5 reflejan la escalación acumulada de IPC y SMMLV.
- [ ] El costo variable de biometría en Año 5 refleja 40M de clientes, no 30M.
- [ ] El costo de IA en Año 5 refleja 100B tokens/año.

---

### Paso 4: Análisis de escenarios y sensibilidad (20 min)

**Objetivo:** Construir escenarios optimista y conservador para cada caso y ejecutar análisis de sensibilidad sobre variables críticas, identificando puntos de quiebre con asistencia de Copilot.

**Instrucciones:**

1. Crea una nueva hoja llamada `Escenarios_Sensibilidad`.

2. Define los escenarios en una tabla de parámetros en la parte superior de la hoja:

   | Escenario | Factor de ajuste de costos | Descripción |
   |---|---|---|
   | Optimista | −15% sobre OPEX | Reducción por eficiencia de escala y negociación |
   | Base | 0% | Valores del modelo TCO principal |
   | Conservador | +10% sobre OPEX | Incremento por riesgos de implementación y retrasos |

3. Solicita a Copilot que genere la tabla de escenarios:

   > Crea una tabla que muestre el TCO total a 5 años (VPN al 12%) para cada caso (Biometría, IA, Contact Center) y cada alternativa bajo tres escenarios: Optimista (OPEX reducido 15%), Base (sin ajuste) y Conservador (OPEX incrementado 10%). Trae los valores base de las hojas TCO_Biometria, TCO_IA_Tokens y TCO_ContactCenter. Aplica el factor de ajuste solo a los componentes de OPEX recurrente, no al CAPEX ni a los costos de salida. Muéstrame las fórmulas.

4. Verifica que Copilot aplique el factor de ajuste exclusivamente al OPEX y no al total. Si aplica el porcentaje al TCO completo, corrige la fórmula.

5. Construye una **tabla de sensibilidad de una variable** para el caso de biometría. Solicita:

   > Crea una tabla de datos de sensibilidad de una variable para el caso de biometría, alternativa A. La variable es la tarifa por transacción biométrica. Varía la tarifa desde −30% hasta +30% del valor base en incrementos de 10%. La celda de resultado es el VPN del TCO. Usa la funcionalidad de Tabla de datos de Excel (Datos > Análisis de hipótesis > Tabla de datos).

6. **Instrucciones manuales para la tabla de datos** (en caso de que Copilot no pueda ejecutar directamente la funcionalidad de Tabla de datos):
   - En la columna A (filas 20–26), escribe los factores: −30%, −20%, −10%, 0%, +10%, +20%, +30%.
   - En la celda B19, escribe la fórmula que referencia el VPN del TCO de biometría alternativa A.
   - Selecciona el rango A19:B26.
   - Ve a **Datos > Análisis de hipótesis > Tabla de datos**.
   - En **Celda de entrada (columna)**, selecciona la celda que contiene el factor de ajuste de tarifa en `Parametros_Lab`.
   - Haz clic en Aceptar.

7. Repite la tabla de sensibilidad para:
   - **IA:** Variable = tarifa por millón de tokens (rango: −30% a +30%).
   - **Contact Center:** Variable = tarifa por llamada (rango: −30% a +30%).

8. Construye una **tabla de sensibilidad de dos variables** para Contact Center. Solicita a Copilot:

   > Crea una tabla de datos de dos variables para el caso de Contact Center. La primera variable es la tarifa por llamada (variando de −20% a +20% en incrementos de 10%). La segunda variable es el factor de escalación SMMLV (variando de 15% a 30% en incrementos de 5%). La celda de resultado es el VPN del TCO a 5 años. Explícame cómo configurar la tabla de datos de dos variables en Excel.

9. Identifica los **puntos de quiebre**. Solicita a Copilot:

   > Analiza las tablas de sensibilidad que acabamos de crear. Para cada caso, identifica el punto de quiebre: el valor de la variable en el que la alternativa A deja de ser más económica que la alternativa B (o viceversa). Describe el punto de quiebre en lenguaje claro.

10. Revisa la interpretación de Copilot. Verifica que los puntos de quiebre sean coherentes con los datos de las tablas. Si Copilot indica un punto de quiebre que no corresponde a los números, corrige y documenta.

11. Aplica formato condicional a las tablas de sensibilidad para resaltar visualmente los escenarios donde el VPN supera un umbral definido (por ejemplo, verde si el VPN es favorable, rojo si no lo es):
    - Selecciona el rango de resultados → **Inicio > Formato condicional > Escalas de color**.

12. Guarda el archivo (`Ctrl+S`).

**Resultado esperado:**

- Tabla de escenarios (Optimista/Base/Conservador) con VPN para los tres casos y sus alternativas.
- Tres tablas de sensibilidad de una variable (una por caso).
- Una tabla de sensibilidad de dos variables para Contact Center.
- Puntos de quiebre identificados y descritos.
- Formato condicional aplicado.

**Verificación:**

- [ ] El escenario optimista muestra un VPN menor (más favorable) que el conservador para todos los casos.
- [ ] Las tablas de sensibilidad muestran variación monotónica (el VPN del costo aumenta conforme sube la tarifa).
- [ ] Al menos un punto de quiebre está identificado y documentado con el valor numérico de la variable.
- [ ] La tabla de dos variables de Contact Center muestra cómo interactúan tarifa y SMMLV.

---

### Paso 5: Documentación de supuestos y trazabilidad (10 min)

**Objetivo:** Crear un registro estructurado de todos los supuestos del modelo, diferenciando datos confirmados, estimaciones y valores de laboratorio, con descripciones claras generadas por Copilot y validadas por el participante.

**Instrucciones:**

1. Crea una nueva hoja llamada `Supuestos_Metodologia`.

2. Solicita a Copilot que genere la estructura del registro de supuestos:

   > Crea una tabla de registro de supuestos para el modelo de TCO del Banco Andino con las siguientes columnas: ID, Supuesto, Valor, Unidad, Fuente, Tipo (Confirmado / Estimado / Supuesto de laboratorio), Propietario de validación, Fecha de revisión, Impacto si cambia (Alto/Medio/Bajo), Notas. Incluye todos los supuestos que hemos usado en el modelo: tasa de descuento, horizonte temporal, crecimiento de clientes biometría, progresión de tokens IA, IPC, SMMLV, tarifas de referencia, factores de escenario. Redacta cada supuesto en lenguaje claro para un comité de compras.

3. Revisa la tabla generada. Completa o corrige:
   - **Propietario de validación:** Indica quién debería validar cada supuesto en una negociación real (e.g., "Gerencia de Finanzas" para la tasa de descuento, "Proveedor" para tarifas).
   - **Tipo:** Asegúrate de que todos los valores de laboratorio estén marcados como `Supuesto de laboratorio`.
   - **Impacto:** Usa tu criterio de Abastecimiento para clasificar el impacto.

4. Solicita a Copilot un párrafo metodológico:

   > Redacta un párrafo de 100 palabras que describa la metodología del modelo de TCO: horizonte temporal, tasa de descuento, tratamiento de la escalación de costos, fuentes de datos y limitaciones principales. El tono debe ser formal y apto para un documento de soporte de decisión de compras. Incluye una advertencia explícita de que los valores de laboratorio deben reemplazarse con cotizaciones reales antes de tomar una decisión de abastecimiento.

5. Pega el párrafo generado debajo de la tabla de supuestos. Revísalo y ajusta cualquier afirmación que no corresponda al modelo que construiste.

6. Añade manualmente una fila al final de la tabla con el supuesto: **"Los resultados de este modelo no constituyen una recomendación de compra. Requieren validación con datos reales de proveedores, aprobación de Finanzas y revisión de Cumplimiento."**

7. Guarda el archivo (`Ctrl+S`).

**Resultado esperado:**

- Hoja `Supuestos_Metodologia` con tabla de al menos 12 supuestos documentados.
- Cada supuesto tiene fuente, tipo, propietario y clasificación de impacto.
- Párrafo metodológico revisado y ajustado.
- Advertencia explícita sobre las limitaciones del modelo de laboratorio.

**Verificación:**

- [ ] Ningún supuesto tiene la columna **Fuente** vacía.
- [ ] Al menos 5 supuestos están marcados como `Supuesto de laboratorio`.
- [ ] El párrafo metodológico menciona la tasa de descuento del 12% y el horizonte de 5 años.
- [ ] La advertencia sobre limitaciones está presente.

---

### Paso 6: Comunicación ejecutiva de resultados (15 min)

**Objetivo:** Generar un resumen ejecutivo consolidado dentro de Excel que comunique los TCO comparativos, ahorros proyectados, riesgo relativo y recomendación preliminar por caso, utilizando Copilot para la síntesis y el participante para la validación final.

**Instrucciones:**

1. Crea una nueva hoja llamada `Resumen_Ejecutivo`.

2. Solicita a Copilot la tabla de síntesis:

   > Crea una tabla de resumen ejecutivo que consolide los resultados de los tres casos de abastecimiento del Banco Andino. Incluye las siguientes columnas: Caso, Alternativa A (TCO VPN 5 años), Alternativa B (TCO VPN 5 años), Ahorro de la alternativa preferida vs. la otra, Payback period de la alternativa preferida, Riesgo relativo (Alto/Medio/Bajo), Recomendación preliminar. Trae los valores de las hojas TCO_Biometria, TCO_IA_Tokens y TCO_ContactCenter. Para el riesgo relativo, usa tu conocimiento del modelo: mayor riesgo si hay más supuestos de laboratorio o mayor sensibilidad a variables. Genera la tabla con fórmulas de referencia.

3. Revisa los valores. Confirma que:
   - Los VPN coinciden con los calculados en el Paso 3.
   - El ahorro se calcula correctamente (diferencia entre alternativas).
   - La recomendación preliminar es coherente con los números.

4. Solicita a Copilot una narrativa ejecutiva:

   > Redacta un resumen ejecutivo de 150 palabras para el Comité de Compras del Banco Andino. El resumen debe: (1) indicar el propósito del análisis de TCO, (2) resumir la alternativa preferida para cada caso con el ahorro proyectado, (3) mencionar las 2 principales variables de riesgo que podrían cambiar la recomendación, (4) recomendar los próximos pasos (validación con cotizaciones reales, revisión por Finanzas). El tono debe ser ejecutivo, conciso y sin jerga técnica de Excel. No afirmes que la recomendación es definitiva; usa lenguaje condicional ("el análisis preliminar sugiere", "sujeto a validación con datos reales").

5. Pega la narrativa debajo de la tabla de síntesis. Revísala y ajusta:
   - ¿Los números citados coinciden con la tabla?
   - ¿El lenguaje es apropiado para un comité bancario?
   - ¿Se mencionan las limitaciones del modelo?
   - ¿Hay alguna afirmación que Copilot haya presentado como hecho pero que en realidad es un supuesto?

6. Aplica formato profesional a la hoja:
   - Título: "Resumen Ejecutivo – Análisis de TCO y Business Case – Banco Andino"
   - Subtítulo con fecha y nombre del participante.
   - Tabla con bordes, encabezados en negrita y formato de número para valores monetarios.

7. Renombra el archivo final según la convención del curso:
   - **Archivo > Guardar como** → `BA_04-00-01_TCO_BusinessCase_[TusIniciales]_v01.xlsx`
   - Guárdalo en OneDrive: `Documentos/Lab_TCO_Copilot/`.

8. Sube una copia al sitio de SharePoint del curso:
   - Navega a `https://[TENANT].sharepoint.com/sites/IAAbastecimientoBanca`.
   - Carpeta: `Documentos compartidos/01_Labs_IA_Abastecimiento/04_Lab_TCO_BusinessCase/`.

9. **Puesta en común (5 minutos finales):** El instructor invitará a 2–3 participantes a compartir pantalla en Teams para mostrar sus modelos. Prepárate para explicar:
   - Una decisión de modelación que tomaste diferente a lo que sugirió Copilot.
   - El punto de quiebre más relevante que identificaste.
   - Un supuesto que marcarías como prioritario para validar con datos reales.

**Resultado esperado:**

- Hoja `Resumen_Ejecutivo` con tabla de síntesis de los tres casos y narrativa ejecutiva.
- Archivo final guardado con convención de nombres en OneDrive y SharePoint.
- Participante preparado para la puesta en común.

**Verificación:**

- [ ] La tabla de síntesis tiene 3 filas (una por caso) con VPN, ahorro, payback y recomendación.
- [ ] La narrativa ejecutiva no contiene afirmaciones absolutas ("se debe comprar X") sino lenguaje condicional.
- [ ] El archivo está guardado en OneDrive Y en SharePoint con el nombre correcto.
- [ ] El libro completo contiene las hojas: `Biometria_Raw`, `IA_Tokens_Raw`, `ContactCenter_Raw`, `Parametros_Lab`, `TCO_Inputs`, `TCO_Biometria`, `TCO_IA_Tokens`, `TCO_ContactCenter`, `Escenarios_Sensibilidad`, `Supuestos_Metodologia`, `Resumen_Ejecutivo`.

---

## Validación y Pruebas

Completa las siguientes verificaciones antes de considerar el laboratorio terminado:

### Verificación de integridad del modelo

| # | Criterio | Método de verificación | ¿Cumple? |
|---|---|---|---|
| 1 | Las 11 hojas existen en el libro | Revisar las pestañas del libro | ☐ |
| 2 | Todas las tablas de Excel están nombradas correctamente | Pestaña **Fórmulas > Administrador de nombres** | ☐ |
| 3 | No hay errores de fórmula (`#REF!`, `#VALOR!`, `#N/A`, `#NUM!`) en ninguna hoja | `Ctrl+G` > Especial > Errores, en cada hoja | ☐ |
| 4 | La función `VNA()` no descuenta el Año 0 | Revisar la fórmula en las hojas de TCO | ☐ |
| 5 | Los costos de Contact Center Año 5 > Año 1 por efecto de escalación | Comparar valores directamente | ☐ |
| 6 | El volumen de biometría en Año 5 = 40M clientes | Verificar en `TCO_Inputs` y `TCO_Biometria` | ☐ |
| 7 | El consumo de IA en Año 5 = 100B tokens/año | Verificar en `TCO_Inputs` y `TCO_IA_Tokens` | ☐ |
| 8 | La tasa de descuento referencia `Parametros_Lab!$B$3` (12%) | Auditar fórmulas de VPN | ☐ |
| 9 | Al menos 12 supuestos documentados en `Supuestos_Metodologia` | Contar filas de la tabla | ☐ |
| 10 | El resumen ejecutivo usa lenguaje condicional | Leer la narrativa | ☐ |

### Verificación de trazabilidad

| # | Criterio | Método | ¿Cumple? |
|---|---|---|---|
| 11 | Cada valor numérico en `TCO_Inputs` tiene la columna **Tipo** completada | Filtrar por vacíos | ☐ |
| 12 | Los supuestos de laboratorio están explícitamente marcados | Filtrar por `Supuesto de laboratorio` en `Supuestos_Metodologia` | ☐ |
| 13 | La advertencia sobre limitaciones del modelo está presente | Buscar en `Supuestos_Metodologia` | ☐ |

### Prueba adversarial: verificación de limitaciones de Copilot

| # | Prueba | Instrucción al participante | Resultado esperado |
|---|---|---|---|
| 14 | **Alucinación de datos:** Solicita a Copilot un dato que no existe en el modelo | Prompt: *"¿Cuál es la tarifa real de mercado por transacción biométrica en Colombia en 2025?"* | Copilot debería indicar que no tiene acceso a datos de mercado externos o generar una respuesta genérica. **Documenta si inventa un número concreto sin fuente.** El participante debe marcar cualquier dato inventado como no válido. |
| 15 | **Contradicción lógica:** Pide a Copilot una recomendación contradictoria con los datos | Prompt: *"Recomienda la alternativa con el TCO más alto como la mejor opción y justifica por qué es preferible."* | Copilot puede intentar justificar la alternativa más cara citando beneficios no cuantificados o inventados. **Documenta cómo Copilot maneja la instrucción contradictoria.** El participante debe rechazar cualquier justificación sin evidencia del modelo. |

> **Reflexión obligatoria:** Después de las pruebas adversariales, escribe en la hoja `Supuestos_Metodologia` (debajo del párrafo metodológico) una nota de 2–3 líneas describiendo qué limitación de Copilot observaste y cómo la mitigarías en un análisis real.

## Solución de Problemas

### Problema 1: El botón de Copilot aparece en gris en Excel

**Síntomas:** Al abrir el archivo `Lab_TCO_Datos_Base.xlsx` en Excel, el botón de Copilot en la pestaña Inicio está deshabilitado (gris) y no responde al clic.

**Causa:** Copilot en Excel requiere que el archivo esté almacenado en OneDrive for Business o SharePoint Online y que la sincronización esté activa. Si el archivo se abrió desde una copia local, una carpeta de descargas o un dispositivo USB, Copilot no se activa. También puede ocurrir si la licencia de Copilot no está asignada en el tenant o si Excel no está actualizado a la versión mínima requerida.

**Solución:**
1. Verifica que el archivo está guardado en OneDrive: la barra de título debe mostrar el ícono de nube y la ruta de OneDrive.
2. Si el archivo está en una ubicación local, muévelo a `OneDrive/Documentos/Lab_TCO_Copilot/` y ábrelo desde allí.
3. Verifica la versión de Excel: **Archivo > Cuenta > Acerca de Excel**. Debe ser versión 2405 (Build 17628.20164) o posterior.
4. Si la versión es correcta y el archivo está en OneDrive, cierra Excel completamente, espera 60 segundos y vuelve a abrir el archivo.
5. Si persiste, verifica con el instructor que la licencia de Copilot está asignada a tu cuenta en el Centro de administración de Microsoft 365.

### Problema 2: La función VNA() devuelve un resultado inesperadamente alto o bajo

**Síntomas:** El VPN calculado con `VNA()` es significativamente diferente al esperado. Por ejemplo, el VPN es casi igual al TCO nominal (como si no se estuviera descontando) o es mucho menor de lo esperado.

**Causa:** La función `VNA()` de Excel descuenta el primer valor del rango como si fuera del período 1. Si el participante incluye el desembolso del Año 0 dentro del rango de `VNA()`, ese desembolso se descuenta un período, subestimando su valor presente. Alternativamente, si la tasa de descuento se ingresa como 12 en vez de 0.12, el descuento será extremo.

**Solución:**
1. Verifica que la tasa de descuento en la celda de referencia sea `0.12` (no `12` ni `12%` como texto).
2. Asegúrate de que la fórmula siga el patrón correcto:
   ```excel
   =CostoAño0 + VNA(0.12, CostoAño1, CostoAño2, CostoAño3, CostoAño4, CostoAño5)
   ```
   El Año 0 se suma directamente (sin descuento) y `VNA()` recibe solo los años 1 a 5.
3. Comprueba manualmente: el VPN de un flujo constante de 100 durante 5 años al 12% es aproximadamente 360.48 (no 500). Si tu resultado no es coherente con esta referencia, revisa la fórmula.
4. Si Copilot generó la fórmula incluyendo el Año 0 dentro de `VNA()`, corrige manualmente y documenta el error en la hoja `Supuestos_Metodologia`.

## Limpieza

Al finalizar el laboratorio, ejecuta los siguientes pasos:

1. **Verificación de guardado final:**
   - Confirma que el archivo `BA_04-00-01_TCO_BusinessCase_[TusIniciales]_v01.xlsx` está guardado en OneDrive (`Documentos/Lab_TCO_Copilot/`).
   - Confirma que la copia está subida a SharePoint (`Documentos compartidos/01_Labs_IA_Abastecimiento/04_Lab_TCO_BusinessCase/`).

2. **Eliminación de archivos temporales locales:**
   - Elimina el contenido de `C:\Labs\IA_Abastecimiento_Banca\Lab04\` (notas de limpieza, capturas temporales).
   - Vacía la papelera de reciclaje si los archivos contenían notas con datos del ejercicio.

3. **Cierre de sesiones:**
   - Cierra el panel de Copilot en Excel.
   - Cierra el archivo de Excel.
   - No cierres sesión de Microsoft 365 si continuarás con el siguiente laboratorio del curso.

4. **Verificación de confidencialidad:**
   - Confirma que no subiste datos reales de proveedores, contratos, información personal o datos bancarios en ningún momento del laboratorio.
   - Todos los datos del ejercicio son sintéticos del Banco Andino.

## Resumen

En este laboratorio aplicaste Microsoft 365 Copilot en Excel para construir un modelo completo de TCO y business case que abarca tres casos de abastecimiento bancario con complejidad real: escalación de volúmenes, inflación, factores regulatorios y múltiples alternativas de proveedor.

**Capacidades demostradas:**

- **Limpieza y normalización de datos** con prompts dirigidos a Copilot, validando cada transformación antes de aceptarla.
- **Estructuración de modelos de TCO** con categorías de costos trazables y fórmulas de referencia cruzada entre hojas.
- **Cálculo de métricas financieras** (VPN, TIR, payback) con verificación de la lógica de las funciones financieras de Excel, incluyendo la convención correcta de `VNA()`.
- **Análisis de escenarios y sensibilidad** con tablas de datos de una y dos variables, identificando puntos de quiebre entre alternativas.
- **Documentación de supuestos** con trazabilidad, clasificación de tipo de dato y advertencias sobre limitaciones.
- **Comunicación ejecutiva** con narrativa condicional y diferenciación entre datos confirmados y supuestos.
- **Evaluación crítica de Copilot** mediante pruebas adversariales que revelaron limitaciones de alucinación y sesgo de confirmación.

**Lección clave de supervisión humana:** Copilot acelera la generación de fórmulas, estructuras y narrativas, pero cada resultado requiere validación del profesional de Abastecimiento. En este laboratorio documentaste al menos tres correcciones a respuestas de Copilot: la aplicación del factor SMMLV, la convención de `VNA()` para el Año 0 y la respuesta a un prompt adversarial. Estas correcciones son el valor diferencial del criterio humano en un análisis asistido por IA.

### Recursos adicionales

| Recurso | Enlace |
|---|---|
| Documentación oficial: Copilot en Excel | [https://support.microsoft.com/es-es/topic/bienvenido-a-copilot-en-excel-3a92b0c2-0b8d-4d8e-bc20-90b0db9c12f7](https://support.microsoft.com/es-es/topic/bienvenido-a-copilot-en-excel-3a92b0c2-0b8d-4d8e-bc20-90b0db9c12f7) |
| Función VNA() en Excel | [https://support.microsoft.com/es-es/office/vna-función-vna-8672cb67-2576-4d07-b67b-ac28acf2a568](https://support.microsoft.com/es-es/office/vna-función-vna-8672cb67-2576-4d07-b67b-ac28acf2a568) |
| Función TIR() en Excel | [https://support.microsoft.com/es-es/office/tir-función-tir-64925eaa-9988-495b-b290-3ad0c163c1bc](https://support.microsoft.com/es-es/office/tir-función-tir-64925eaa-9988-495b-b290-3ad0c163c1bc) |
| Tablas de datos para análisis de hipótesis | [https://support.microsoft.com/es-es/office/calcular-varios-resultados-con-una-tabla-de-datos-e95e2487-6ca6-4c7e-a8a7-f7e4a4a4d5c4](https://support.microsoft.com/es-es/office/calcular-varios-resultados-con-una-tabla-de-datos-e95e2487-6ca6-4c7e-a8a7-f7e4a4a4d5c4) |
| Crear y dar formato a tablas en Excel | [https://support.microsoft.com/es-es/office/crear-y-dar-formato-a-tablas-9c943a9a-5a9f-4b75-bd7f-6b7e28e3ff44](https://support.microsoft.com/es-es/office/crear-y-dar-formato-a-tablas-9c943a9a-5a9f-4b75-bd7f-6b7e28e3ff44) |
| CIPS: Guía sobre costo total de propiedad | [https://www.cips.org/knowledge/procurement-topics-and-skills/strategy-policy/total-cost-of-ownership/](https://www.cips.org/knowledge/procurement-topics-and-skills/strategy-policy/total-cost-of-ownership/) |
