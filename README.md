# EarthQuake — Monitor sísmico multiagencia

Aplicación web de monitorización sísmica y alertas, en un único archivo HTML. Combina catálogos de terremotos, boletines oficiales, EEW, observaciones de estaciones, mapas meteorológicos y otros paneles ambientales. Los datos dependen de la disponibilidad y las condiciones de sus proveedores; que una fuente aparezca en el código o en la interfaz no garantiza que esté respondiendo en todo momento.

## Novedades de esta edición

- Los marcadores circulares originales de estaciones japonesas usan la paleta instrumental `KyoshinShindoColorMap` en los códigos de feed correspondientes. El cambio se limita al color de esos círculos: no modifica su tamaño, forma, ubicación ni datos.
- Los puntos numerados de intensidad SREV/Sesna quedan separados de los círculos de estaciones y conservan su estilo y comportamiento.
- Se conserva la visualización existente de estaciones Yahoo/Kyoshin y NIED K-NET/KiK-net, junto con la selección de fuente y las métricas que ya tenía el HTML.
- No se incorpora S-Net ni se agrega un acceso/botón S-Net en esta versión. Las descargas WIN32 de NIED son archivos de ondas para intervalos concretos, no un flujo continuo integrado al monitor; el uso y la redistribución deben respetar las condiciones de NIED.
- Se conserva la barra de herramientas existente para Inicio, Japón/NIED, alertas meteorológicas JMA, Ajustes y Mar de Japón. No se añadieron controles nuevos de S-Net.

## Funciones principales

### Mapa y navegación

- Mapa Leaflet con controles y herramientas integrados en el HTML.
- Mapas base: estilo oscuro SesnaQuake/EOX Sentinel-2, oscuro, satélite Esri y terreno.
- Opciones para color del mar, fallas tectónicas y satélites meteorológicos GOES-East, GOES-West y Himawari.
- Capas opcionales de viento, rayos (Blitzortung) y radar meteorológico NOAA.
- La aplicación enfoca sismos nuevos o seleccionados según la vista activa, conserva apartados prioritarios y evita saltos causados por actualizaciones repetidas.
- Reloj y contador de sismos del día.

### Catálogo sísmico multiagencia

- Lista de sismos con filtros de magnitud, agencia, región y sismos sentidos; selección y enfoque del evento.
- Agencias y catálogos reconocidos por los selectores del HTML incluyen USGS/NEIC, JMA, CENC, EMSC, IGN, INETER/CATAC, GEOFON/GFZ, SSN, AFAD, BMKG, GeoNet, INGV, IPGP, SED, PHIVOLCS, CSN, IG-EPN, HKO, VMGD, NOA, KOERI, BCSF, NRCan, USP, MMD, CEA-PR y SGC, además de fuentes de alerta como Early-Est, ShakeAlert y GDACS.
- Los conectores y feeds se manejan por separado; se usan respaldos de transporte/proxy cuando están programados. Un error o una respuesta vacía no debe interpretarse como que no ocurrió un sismo.
- La interfaz conserva la agencia de origen y distingue eventos preliminares, revisiones, informes finales y alertas tempranas cuando la fuente ofrece esos estados.
- Presentación de horas adaptada a Colombia (UTC−5); los nombres y datos originales de las agencias se conservan donde corresponde.

### Intensidad, observaciones y estaciones

- Dibujo de la intensidad oficial de JMA del evento seleccionado cuando está disponible; se muestran las estaciones e intensidades oficiales asociadas al boletín, sin agregar un catálogo JMA ficticio.
- Intensidad observada/estimada de fuentes compatibles, con leyendas y escalas diferenciadas. Puede seleccionarse la escala nativa de la agencia, Shindo, MMI, CSIS, CWA o GeoNet MMI según la capa y sus datos.
- GeoNet permite activar observaciones Strong Motion recientes y seleccionar intensidad MMI, PGA o PGV cuando la fuente las entrega.
- Japón: estaciones Yahoo/Kyoshin CDN y NIED K-NET/KiK-net; el usuario puede elegir Yahoo, NIED, K-NET, KiK-net o Yahoo + NIED. Hi-net aparece como catálogo sin telemetría; F-net y V-net se identifican explícitamente como sin flujo público verificado en esta capa.
- Los círculos de las estaciones japonesas usan la paleta instrumental Kyoshin en esta edición. Los marcadores numerados de intensidad SREV/Sesna no se alteran por ese ajuste.
- La leyenda de Japón distingue la escala 0–7 y las subdivisiones 5−, 5+, 6− y 6+ cuando corresponden. Los valores derivados de colores se etiquetan como aproximados y no como PGA/PGV crudos u oficiales.
- Detector local Yahoo/NIED: se basa en tramas frescas de estaciones; requiere confirmación espacial/temporal y separa movimiento instrumental de un sismo oficial. La pérdida del feed no equivale a reposo y el centroide no se presenta como epicentro confirmado.
- Vista del Mar de Japón y medidas máximas NIED disponibles en el monitor.
- Taiwán: módulo TREM y módulo P-Alert con estados y métricas visibles en sus apartados cuando llegan datos. PGA/PGV se muestran solo si se reciben; PGD no se inventa.
- EarthScope: capas regionales con muestras recientes para Colombia, Costa Rica, México, Guatemala, El Salvador, Nicaragua, Chile, Brasil, Taiwán, Argentina, Puerto Rico, República Dominicana, Haití, Alaska y Estados Unidos continental; se pueden activar/desactivar por región.
- Capas adicionales con interruptores propios: RSBR (Brasil), GEOFON/GFZ regional y TexNet (Texas). La telemetría reciente y las estimaciones instrumentales se diferencian de intensidad oficial, PGA/PGV calibrados y detección de sismos.
- Conexión opcional EarthScope SeedLink. La interfaz comunica el estado de conexión y no considera que la opción habilitada pruebe por sí sola que exista una trama válida.
- Estaciones KMA PEWS se usan para el procesamiento de la fuente/EEW, pero el código actual desactiva el dibujo de sus puntos en el mapa.

### EEW, ondas y alertas sísmicas

- Manejo de alertas tempranas de las fuentes integradas, con tarjeta/panel de alerta, revisiones y estados diferenciados de alerta, información y cancelación según el origen.
- EEW JMA a través de los canales disponibles en el HTML, incluido Wolfx, con presentación y reglas de vigencia propias; el catálogo JMA no se confunde con un EEW.
- Dibujo de frentes P/S teóricos con TauP (modelo IASP91) para eventos que permiten ese cálculo. Hay modos preciso, rápido y respaldo; el respaldo geométrico se identifica como estimación, no como TauP.
- Visualización de ondas para alertas elegibles; los frentes calculados son estimaciones y no formas de onda recibidas en estaciones.
- Alertas específicas de JMA, CWA, KMA PEWS y otras fuentes se conservan diferenciadas; una magnitud, lugar, intensidad, profundidad u hora ausente no se debe completar con un valor inventado.
- Informe final de intensidad JMA y aviso EEW son etapas distintas; el cierre de la alerta no elimina el evento confirmado de la lista.
- El monitor evita repetir alertas o sonidos por cada sondeo de la misma revisión.

### Avisos oficiales de Japón

- Avisos meteorológicos JMA en apartado propio, con categorías/colores según la información oficial y polígonos de zonas de pronóstico cuando están disponibles.
- Boletines volcánicos JMA en sección propia y procesamiento de productos JMA relacionados.
- Alertas, avisos y pronósticos de tsunami JMA, junto con boletines PTWC/NTWC/NOAA disponibles en el módulo. Se distingue entre alerta/aviso y cambios menores o pronósticos.
- Sismos JMA e información de intensidad, con traducción/presentación al español en los módulos de aviso y horario local de Colombia.
- El apartado de estaciones Japón/NIED no agrega S-Net; el botón visible es el acceso existente de Japón/NIED y no un control de S-Net.

### Tiempo severo, ciclones y desastres

- Tifones/ciclones tropicales: panel cartográfico con fuentes incluidas en el HTML (JMA, NMC/CMA y otros proveedores programados), trayectorias e información disponible.
- Huracanes de Estados Unidos: módulo NOAA/NHC con información oficial y geometría cuando el feed la publica.
- Alertas meteorológicas oficiales de Estados Unidos/NWS, con radar NOAA y referencias a condados cuando están disponibles.
- Alertas globales GDACS para peligros cubiertos por su servicio, en apartado independiente.
- Alertas ambientales mundiales de clima espacial NOAA/SWPC y protección civil/GDACS en su panel específico.
- Volcanes: seguimiento/panel mundial con fuentes volcánicas incorporadas y marcadores informativos. La interfaz diferencia alertas/observaciones de un catálogo de volcanes.
- SIAT-CT México: vista del aviso y mapa oficial de ciclones tropicales, con opción de abrir la fuente oficial y actualizar.

### Colombia: movilidad, clima, noticias y fútbol

- Movilidad Bogotá: apartado con información de la Secretaría Distrital de Movilidad y componentes Waze e INVÍAS, además de avisos por categorías como accidente, manifestación, cierre, TransMilenio, clima y tráfico. Waze se identifica como información de usuarios, no como boletín oficial de la SDM.
- Consulta/visualización de avisos y fuentes de movilidad existentes en el HTML; la primera carga de una fuente no se presenta como una novedad nueva.
- Clima: condiciones meteorológicas y búsqueda de ciudades con Open-Meteo, con consulta de datos actuales, viento y variables disponibles.
- Noticias/avisos colombianos: agregación de titulares de fuentes incorporadas y panel de alertas ambientales; no se fabrican titulares cuando un feed falla.
- Próximo partido de la Selección Colombia, incluidos encuentros de futsal cuando están disponibles en la fuente FCF. El marcador y eventos solo se muestran cuando la fuente los entrega; la integración no convierte fixture de calendario en goles en vivo.
- Alertas configurables de goles, descanso y final, y efecto visual de lluvia de balones por gol cuando está activado.

### Audio, voz y notificaciones

- TTS configurable, selección/prueba de voz y volumen general ajustable.
- Sonidos de avisos sísmicos, intensidad y tsunami según los módulos; opciones de sonido y notificaciones en Ajustes.
- Ticker/telop informativo para avisos elegibles, con reglas de antigüedad y prioridad por tipo de producto.
- Notificaciones push opcionales, sujeto a navegador compatible, permiso y disponibilidad del servicio; no son un sistema EEW ni garantizan entrega instantánea.

### Ajustes y visualización

- Ajuste de magnitud mínima del catálogo y del ticker, región, agencia, escala de intensidad, mapa, modelo TauP, voz, sonidos, volumen, estaciones y capas regionales.
- Interruptores para fallas, notificaciones del navegador, GeoNet, estaciones de Japón, TREM/P-Alert, métricas NIED y capas EarthScope/RSBR/GFZ/TexNet.
- Diseño adaptable a escritorio y móvil. La interfaz integra lista, mapa, paneles de fuentes y controles de herramientas.

## Límites importantes

- La información es de monitorización, no sustituye a los organismos oficiales ni a los sistemas públicos de protección civil.
- “Estimado”, “instrumental”, “aproximado” y “oficial” no son intercambiables. PGA/PGV/PGD solo se presentan como mediciones cuando una fuente los entrega; conversiones visuales deben permanecer marcadas como aproximadas.
- Un punto de catálogo de estación no demuestra telemetría reciente. La conexión se debe respaldar con tramas frescas y válidas.
- La señal de un detector local no crea por sí sola un sismo confirmado, magnitud, profundidad o epicentro oficial.
- Las dependencias de red, CORS, servicios de terceros, workers/proxies y navegadores pueden afectar feeds, mapas, capas y notificaciones.
- Esta edición no integra estaciones ni ondas S-Net. Las formas de onda WIN32 de NIED descargadas por el usuario son datos de intervalos específicos y no se redistribuyen por medio de este HTML.

## Créditos y licencias

- El HTML incorpora Leaflet y mantiene avisos de licencia/atribución de sus componentes y fuentes.
- La cabecera del archivo declara **AGPL-3.0-or-later** para esta copia y señala componentes derivados/adaptados de SesnaQuake (Domiko7), incluyendo elementos visuales, panel de eventos, marcadores de estaciones, símbolos de intensidad y presentación EEW. Si se publica o redistribuye una versión modificada, hay que cumplir la licencia AGPL-3.0 y ofrecer el código fuente correspondiente.
- Los sonidos SREV atribuidos en el HTML son de kotoho7 y se indican bajo CC BY-SA 2.0.
- Los mosaicos, observaciones, intensidades, feeds y otros activos conservan sus términos y atribuciones originales; revisar las condiciones de cada proveedor antes de reutilizar o redistribuir.
- Los nombres de agencias y marcas se usan para identificar sus datos y servicios, no implican respaldo de sus titulares.

## Archivo

Esta documentación describe el HTML independiente de EarthQuake entregado junto con este README. Las fuentes externas pueden cambiar; el comportamiento efectivo corresponde siempre al código y los feeds disponibles en la versión concreta del archivo.
