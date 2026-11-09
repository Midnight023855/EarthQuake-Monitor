# EarthQuake — variante móvil ligera

README de `EarthQuake_Japan_movil_ligero_Intensidad_fija_movimiento_TTS_Mangxu.html`. Esta variante está pensada para reducir trabajo no crítico en teléfonos compatibles, manteniendo activas las fuentes de EEW. Documenta lo presente en este archivo, no todas las funciones ni diferencias del HTML principal.

> No se verificó la interfaz en un teléfono ni se probó audio real. La conectividad y las voces disponibles dependen del dispositivo, el navegador y los servicios externos.

## Novedades de esta versión

- **TTS de informes sísmicos por idioma de agencia**, activable o silenciable en **Ajustes → Sonido y TTS**. La opción es independiente del audio general y guarda su preferencia.
- La locución se limita a informes sísmicos nuevos elegibles; no se usa para EEW, tsunami, volcanes ni meteorología. El TTS requiere soporte de `SpeechSynthesis` y voces compatibles instaladas en el dispositivo.
- Formatos de voz implementados para **BMKG** (indonesio), **JMA** (japonés), **CWA** (chino tradicional de Taiwán), **GeoNet** (inglés de Nueva Zelanda, para informes de calidad final), **CENC** y **CEIC** (chino simplificado). Son locuciones construidas por el monitor a partir de los campos disponibles; no son audio oficial de las agencias ni una garantía de reproducción exacta de sus boletines.
- **CEIC:** la ficha grande identifica el reporte como “CEIC Report” junto a la hora.
- **Catálogos Mangxu:** se incorporaron CEA-PR, AusPass, IPMA, RSN Costa Rica, INFP y CEIC. Se muestran como datos agregados de Mangxu, no como conexión directa verificada con cada agencia. El snapshot de CEA-PR es catálogo, no una trama EEW activa.
- **Conexiones más estrictas:** la etiqueta “Conectada” ya no se mantiene por una caché o por un estado antiguo. Para las fuentes HTTP genéricas y Mangxu requiere una respuesta válida reciente; los WebSockets se juzgan por actividad reciente. En Mangxu, una respuesta válida sin eventos recientes también puede significar que el servicio respondió, no que haya sismos nuevos.
- **SGC:** actualmente no conecta de forma verificable. El feed consultado devolvió HTTP 403 `AccessDenied` en las comprobaciones realizadas, y el respaldo FDSN no respondió. No se deben tratar datos guardados en caché como conexión activa ni confundir una fuente distinta con el SGC.

## Funciones presentes

### Monitor sísmico y mapa

- Mapa interactivo y lista de sismos multiagencia, con selección de eventos y fichas de detalle.
- Conserva la identificación de agencia/fuente y separa los reportes sísmicos, alertas tempranas y detecciones instrumentales. La selección de una fuente en la lista no garantiza que esté disponible en ese momento.
- Visualización de las fuentes sísmicas y paneles integrados en este HTML; los eventos de Mangxu se identifican como agregados.
- Presentación de hora en la interfaz según las reglas implementadas por el monitor; las locuciones TTS usan las zonas horarias propias configuradas para las agencias indicadas.

### Intensidad, detección y alertas

- Intensidad JMA, estaciones/observaciones japonesas y detección de movimiento conforme a los módulos incluidos en el archivo.
- Integraciones TREM y P-Alert de Taiwán y sus herramientas de detección/observación. Una detección de movimiento instrumental no equivale a un epicentro oficial, una intensidad oficial ni una alerta temprana gubernamental.
- EEW y frentes de ondas P/S calculados donde hay datos suficientes. Las ondas calculadas son estimaciones, no señales sísmicas medidas directamente.
- Alertas de tsunami, tifones y otros módulos ambientales incorporados en la variante. La presencia de un panel no garantiza datos actuales de su proveedor.
- Perfiles de rendimiento móvil reducen algunas tareas no críticas en dispositivos que cumplen los criterios declarados en los metadatos del HTML. No se afirma una tasa de cuadros ni estabilidad garantizada en un modelo concreto de teléfono.

### Audio y ajustes

- Controles de sonidos y volumen general.
- Interruptor específico para TTS de informes sísmicos en Ajustes. Silenciar el TTS no implica apagar sonidos de alerta.
- No se habla información estimada como si fuera una medición oficial. Las reglas de elegibilidad pueden omitir reportes a los que falten campos necesarios o cuya calidad no cumpla el criterio correspondiente.

## Fuentes agregadas de Mangxu

Se consultan los catálogos de:

- CEA-PR
- AusPass
- IPMA
- RSN Costa Rica
- INFP
- CEIC

El monitor prioriza el respaldo usado para sortear la falta de CORS de Mangxu en navegadores móviles y puede recurrir a la consulta directa como alternativa. La marca de conexión indica una respuesta válida reciente del feed, no frescura de cada evento, confirmación por la agencia de origen ni aprobación de uso para protección civil. Los eventos deben conservar su atribución de fuente agregada.

## Estado de conexión: cómo interpretarlo

- La etiqueta es una señal técnica de respuesta reciente o WebSocket activo, no una evaluación de calidad científica ni una garantía de disponibilidad futura.
- Las fuentes con caché pueden seguir mostrando eventos anteriores aunque estén desconectadas; los eventos almacenados no renuevan por sí solos la conexión.
- Algunos catálogos pueden responder correctamente y no contener sismos recientes. “Conectada” no quiere decir “hay sismos nuevos”.
- Los límites de tiempo y el método de comprobación varían según la fuente. CORS, servicios proxy, redes móviles, el navegador o el proveedor pueden impedir consultas aunque el endpoint esté disponible desde otro entorno.
- El estado SGC debe considerarse desconectado mientras su endpoint no responda por una ruta oficial verificable.

## Límites y uso responsable

- Este monitor es una herramienta informativa y no sustituye a las agencias oficiales ni las instrucciones de protección civil.
- “Oficial”, “agregado”, “estimado”, “aproximado” e “instrumental” no son equivalentes. No se deben inferir intensidades oficiales, PGA/PGV/PGD medidos, epicentros confirmados ni alertas activas a partir de datos ausentes.
- Las consultas externas pueden cambiar, bloquearse o dejar de responder. La disponibilidad real debe comprobarse en el dispositivo donde se ejecuta el HTML.
- Las voces dependen de las capacidades del navegador y de los paquetes de voz instalados; no se verificó pronunciación ni reproducción en dispositivos físicos.

## Licencias y atribución

- El HTML conserva los avisos de licencia y atribución incluidos en el propio archivo. La cabecera declara componentes derivados/adaptados de SesnaQuake bajo **AGPL-3.0**; al redistribuir o publicar modificaciones, revisa y cumple las obligaciones aplicables y proporciona el código fuente correspondiente cuando la licencia lo exige.
- Leaflet, servicios de mapas, agencias, feeds agregados, sonidos y demás datos/componentes pueden tener condiciones propias. Consulta las licencias y términos vigentes antes de reutilizarlos o redistribuirlos.

## Archivo descrito

`EarthQuake_Japan_movil_ligero_Intensidad_fija_movimiento_TTS_Mangxu.html`
