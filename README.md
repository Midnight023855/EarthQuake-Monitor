# EarthQuake — Monitor sísmico multiagencia

Monitor web en un único archivo HTML para consultar sismos, alertas tempranas, observaciones de estaciones y avisos ambientales. El mapa y los paneles reúnen productos de distintas agencias, pero cada dato conserva su fuente y tipo: una detección instrumental no equivale a un sismo confirmado, y una estimación no equivale a una medición oficial.

> La disponibilidad depende de las agencias, servicios, conexiones, workers/proxies y permisos del navegador. Un estado de conexión o una respuesta HTTP exitosa no garantiza por sí solo que el dato sea reciente.

## Novedades de esta edición

- **Intensidad sísmica JMA por ciudad:** el mapa del sismo seleccionado puede colorear las ciudades afectadas con los niveles oficiales de Shindo publicados por JMA. No colorea prefecturas completas ni inventa áreas cuando el informe no las proporciona.
- **Estaciones JMA con marcadores Sesna/SREV:** las observaciones oficiales de las estaciones se muestran como puntos numerados con el símbolo de intensidad Sesna/SREV, igual al estilo empleado para estaciones NIED. Los valores, colores y ubicaciones proceden del informe JMA asociado; no son estaciones añadidas de un catálogo.
- **Render optimizado de mapas JMA:** las geometrías municipales se agrupan por nivel de intensidad para reducir capas y trabajo de dibujo. Las alertas meteorológicas también agrupan las geometrías oficiales por nivel/estilo, conservando sus límites y severidad. No se ha documentado aquí un benchmark de rendimiento ni una prueba visual en todos los dispositivos.
- **Preliminar y final JMA:** los informes preliminares permanecen en la lista; cuando llega el informe final asociado, el flujo actualiza la misma entrada/ficha en lugar de tratarlo como un evento nuevo sin relación. La asociación usa los identificadores/datos de los informes disponibles; no se completa información ausente con valores inventados.
- **Apartados automáticos:** el recorrido opcional no se reanuda silenciosamente desde una preferencia antigua al cargar, y se excluyen pasos de recorrido que solo mostraban una capa de mapa sin una ficha útil. Las alertas nuevas de los módulos siguen teniendo sus propios criterios de apertura.
- **TTS eliminado por completo:** se retiraron la síntesis de voz, anuncios hablados, colas de voz, selección/prueba de voz y sus controles. Se conservan los sonidos de alerta y el ajuste de volumen general.
- **Fuentes retiradas:** PancakesAPI, UNGRD e IDEAM ya no forman parte de esta edición. También se retiraron las capas/módulos de EarthScope, RSBR, TexNet y las capas de estaciones GEOFON/GFZ; el catálogo sísmico GEOFON/GFZ, cuando está disponible, es independiente.
- **Movilidad Bogotá:** el HTML contiene un apartado integrado de movilidad con mapa, localidades, categorías de avisos, accesos a Waze e INVÍAS y un módulo de vehículos de TransMilenio servido mediante Worker. Los datos de buses deben mostrarse con su hora real reportada; una respuesta exitosa o datos atrasados no se deben describir como telemetría en vivo.
- **NDMA Japan:** panel integrado para consultar reportes y avisos de NDMA, separado de los productos JMA. Las geometrías solo representan una afectación cuando el reporte aporta geometría oficial; las capas GSI opcionales son referencias generales de riesgo, no afectaciones atribuidas al aviso.

## Funciones

### Mapa, navegación y ajustes

- Mapa interactivo basado en Leaflet, con lista de sismos, selección de evento, paneles y controles integrados.
- Bases y opciones de mapa presentes en Ajustes: EOX Sentinel-2, satélite Esri y terreno; tema/color del mar; líneas de fallas PB2002; capas meteorológicas disponibles en el HTML.
- Reloj en hora de Colombia y controles de enfoque/retorno. La navegación evita que las actualizaciones repetidas desplacen el mapa sin necesidad.
- Filtros de lista por magnitud, región y sismos sentidos; selección de agencias visibles y opciones para definir el zoom de los sismos de la lista.
- Ajustes de intensidad, modelo TauP, estaciones y métricas; las preferencias se guardan en el navegador.
- El recorrido de secciones es opcional. El usuario puede activarlo desde el control meteorológico; no se inicia por sí solo tras cargar una preferencia antigua.

### Catálogo sísmico y reportes

- Lista multiagencia con información de eventos y, cuando la fuente la ofrece, distinción entre reporte preliminar, revisión, informe final y alerta temprana.
- Las agencias disponibles en el selector de lista incluyen USGS/NEIC, JMA, CENC, CEA, CEIC, EMSC, IGN, INETER, GEOFON, SSN, AFAD, BMKG, GeoNet, INGV, IPGP, SED, PHIVOLCS, CSN, IG-EPN, Early-Est, HKO, VMGD, NOA, KOERI, SGC, KMA, BCSF, NRCan, USP, MMD y CEA-PR. La presencia en el selector no garantiza que cada fuente responda en todo momento.
- Se preservan agencia, nombres y datos de origen cuando corresponde; las horas de interfaz se presentan en la zona horaria de Colombia.
- Las respuestas de error, feeds vacíos y respaldos de red no deben interpretarse como confirmación de que no hubo un sismo.

### Intensidad, estaciones y movimiento instrumental

- **JMA:** al seleccionar un evento con informe oficial compatible, se dibujan las ciudades con intensidad publicada y los puntos de estaciones de observación del mismo informe. Los puntos usan marcadores numerados Sesna/SREV. Si el informe no incluye un dato, no se fabrica.
- **Alertas meteorológicas JMA:** se muestran polígonos municipales/áreas afectadas y sus niveles oficiales cuando el boletín los aporta. La geometría se agrupa por estilo para reducir la cantidad de capas dibujadas.
- **Japón — Yahoo/Kyoshin y NIED K-NET/KiK-net:** selección disponible para Yahoo, NIED, K-NET, KiK-net o ambas fuentes; se pueden consultar los cuadros de intensidad/PGA/PGV estimados de NIED. Hi-net y F-net se identifican como catálogo sin telemetría integrada en esta vista; V-net no se presenta como flujo público verificado.
- Las lecturas aproximadas de PGA/PGV derivadas de color se identifican como aproximadas; no son medidas crudas. La pérdida de datos o un feed detenido no equivale a reposo confirmado.
- La detección local Yahoo/NIED se distingue de una alerta oficial: los grupos/centros instrumentales no se presentan como epicentros oficiales ni generan magnitudes confirmadas.
- **Taiwán:** módulos TREM y P-Alert para observaciones y detección local. Intensidad instrumental, PGA y PGV se muestran solo cuando la fuente entrega datos; PGD no se inventa. Movimiento detectado por estaciones no es por sí mismo EEW oficial ni intensidad Shindo oficial.
- **GeoNet:** vista de observaciones Strong Motion recientes y puntos asociados a un sismo seleccionado, con intensidad MMI, PGA o PGV según el producto disponible. Los productos horarios y los puntos de un evento se mantienen separados.
- Las capas agrupadas de ciudades JMA y alertas meteorológicas reducen el número de geometrías renderizadas; no alteran la severidad o ubicación oficial de los polígonos.

### Alertas sísmicas y ondas

- Paneles para EEW y avisos de las fuentes implementadas, con revisiones y estados diferenciados según el producto de origen.
- EEW JMA integrado a través de Wolfx con las rutas/respaldo presentes en el HTML; el aviso de EEW se distingue del catálogo de sismos confirmados.
- Cálculo y dibujo de frentes P/S estimados con TauP cuando el evento y los datos permiten el cálculo. Los frentes teóricos no son formas de onda recibidas por estaciones.
- Los estados, coordenadas, magnitud, profundidad e intensidad se muestran solo si los proporciona el origen o una estimación identificada como tal.
- Se conservan sonidos de avisos sísmicos y de otros eventos. **No hay síntesis de voz ni anuncios hablados.**

### Japón: JMA y NDMA

- Sismos JMA, informes de intensidad, alertas tempranas JMA y boletines volcánicos JMA en flujos/paneles separados.
- Actualización de la entrada preliminar cuando se recibe el informe final correspondiente, en vez de borrar el preliminar antes de que llegue el informe posterior.
- Avisos meteorológicos JMA con niveles/colores publicados y geometrías de las zonas afectadas cuando están disponibles.
- Mapas de intensidad sísmica por ciudades y observaciones de estaciones, con puntos numerados Sesna/SREV de intensidad oficial.
- Apartado NDMA Japan para avisos y publicaciones de gestión de desastres. NDMA no se confunde con JMA; las capas opcionales de riesgo GSI no son polígonos de afectación del aviso.
- Avisos de tsunami JMA y boletines PTWC/NTWC/NOAA disponibles en el módulo correspondiente.

### Alertas meteorológicas, tsunami y ambientales

- Seguimiento cartográfico de tifones/ciclones tropicales, incluyendo productos JMA/NMC y proveedores contemplados por el código.
- Panel NOAA/NHC para sistemas tropicales y módulo NWS para alertas meteorológicas de Estados Unidos; incluye los detalles/zonas publicados por el feed y el radar NOAA disponible en la vista.
- Avisos de tsunami JMA y productos PTWC/NTWC/NOAA, con áreas y geometrías solo cuando el producto las entrega.
- Alertas globales GDACS en su apartado cartográfico y panel separado de clima espacial NOAA/SWPC.
- Vista de avisos volcánicos mundiales y apartados volcánicos JMA y Colombia/Caribe cuando hay datos de las fuentes integradas.
- SIAT-CT México: módulo para nuevos avisos de ciclón tropical con enlace al boletín oficial y geometrías del servicio cuando están disponibles.
- Un sondeo repetido de una alerta existente no se trata automáticamente como novedad nueva.

### Colombia: movilidad y otras herramientas

- **Movilidad Bogotá:** apartado con mapa y localidades, avisos por categorías como accidentes, manifestaciones, cierres, TransMilenio, clima y tráfico, además de accesos a Waze e INVÍAS.
- **TransMilenio:** consulta a través del Worker configurado; las fichas deben conservar la hora de reporte real. Si el proveedor devuelve un corte antiguo, no se debe llamar “en vivo”.
- Vista Colombia/Caribe para reportes volcánicos y de tsunami, con accesos a las fuentes incorporadas.
- Búsqueda meteorológica de ciudades y consulta de condiciones actuales disponibles mediante Open-Meteo.
- Seguimiento de partidos de Colombia y avisos/efectos configurables cuando los datos del servicio están disponibles. El monitor no debe inferir goles a partir de un calendario sin marcador real.

### Audio, notificaciones y presentación

- Controles para habilitar sonidos y ajustar el volumen general; sonidos incorporados SREV y sonidos de interfaz.
- Notificaciones del navegador opcionales, sujetas a permiso del usuario, compatibilidad y disponibilidad.
- Ticker informativo y textos en pantalla en español en los módulos que los implementan; la traducción visible no depende de TTS.
- Diseño con reglas adaptativas de pantalla; el rendimiento debe verificarse en el dispositivo concreto y no se garantiza una tasa de cuadros determinada.

## Fuentes retiradas de esta edición

No se deben documentar como funciones activas las integraciones retiradas de PancakesAPI, UNGRD, IDEAM, EarthScope, RSBR y TexNet, ni las capas de estaciones GEOFON/GFZ. El catálogo sísmico GEOFON/GFZ se conserva por separado de esas capas. Esta edición tampoco incluye TTS.

## Límites y lectura responsable

- Este monitor no sustituye las instrucciones de organismos oficiales ni servicios públicos de protección civil.
- “Oficial”, “instrumental”, “estimado” y “aproximado” tienen significados diferentes. Un cálculo o detector local no crea un sismo confirmado, una magnitud oficial o un epicentro oficial.
- La existencia de un punto en un catálogo no prueba que esa estación esté transmitiendo ahora. Solo las tramas recientes y válidas respaldan una afirmación de telemetría actual.
- Las capas de riesgo generales no deben atribuirse a un evento concreto si el informe no incluye geometría de afectación.
- Las fuentes externas, workers/proxies, CORS, servicios de mapas y permisos pueden cambiar o dejar de responder. Los datos atrasados deben mostrarse con su hora real, no como datos en vivo.

## Créditos y licencias

- La cabecera del HTML declara **AGPL-3.0-or-later** y reconoce componentes derivados/adaptados de SesnaQuake. Al redistribuir/publicar una versión modificada, revisa y cumple las obligaciones aplicables de la licencia, incluida la disponibilidad del código fuente correspondiente.
- Los sonidos SREV se atribuyen en el HTML a kotoho7 bajo **CC BY-SA 2.0**.
- Leaflet, EOX Sentinel-2, Esri, JMA, GeoNet, agencias sísmicas, productos meteorológicos y demás datos conservan sus licencias, atribuciones y términos originales. Verifica las condiciones de cada proveedor antes de reutilizar o redistribuir sus datos.

## Archivo descrito

Este README documenta `EarthQuake_Japan_motion_wave_close_10s.html`, el HTML principal de esta edición. No describe ni sustituye `EarthQuake_Japon_Completo.html`, que es una variante independiente. Las capacidades efectivas son las que contiene el HTML distribuido; no se debe inferir que una fuente funciona solo porque figure en la documentación o la interfaz.
