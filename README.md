# EarthQuake ligero — monitor sísmico en un HTML

README de `EarthQuake_Ligero_animaciones_JapanMonitor.html`. Esta edición reúne un mapa sísmico multiagencia, herramientas de consulta y módulos de observación instrumental. La disponibilidad depende de las fuentes externas, del navegador y de sus permisos.

> **Estado de verificación:** se revisó estáticamente el HTML y la sintaxis de algunos controladores. No se validó en navegador ni en teléfono que todas las vistas, conexiones, alertas o temporizadores funcionen de extremo a extremo. La presencia de una agencia en la interfaz no garantiza que su fuente conecte.

## Funciones presentes

### Mapa, lista y ajustes

- Mapa interactivo Leaflet con una lista de sismos, fichas de evento y controles de navegación.
- Selector de agencias y filtros de lista, incluidos magnitud, región, sismos sentidos y nivel de zoom de selección.
- Reloj y hora local de Colombia en los módulos correspondientes.
- Ajustes de audio, volumen general, idioma de interfaz, modelo TauP, mapa, estaciones de Japón, detectores locales y métricas disponibles.
- Fuentes cartográficas, capas y servicios externos dependen de su disponibilidad y condiciones de uso.

### Catálogo de sismos

El HTML incorpora funciones de consulta para varias agencias y agregadores, entre ellas USGS/NEIC, JMA, CENC, EMSC, INGV, NOA, KOERI, GeoNet, BMKG, CSN, IG-EPN, SSN, PHIVOLCS, AFAD, INETER, GEOFON/GFZ, SGC y otros catálogos que aparecen en la lista o el código.

- Se conserva la atribución de agencia cuando está presente en los datos.
- Algunos resultados provienen de agregadores; no equivalen a una conexión directa con la agencia indicada.
- Los datos pueden tener revisiones y retrasos. Una fuente caída, una respuesta vacía o un evento guardado en caché no confirma que no haya ocurrido un sismo ni que la conexión esté activa.
- La lista de agencias en pantalla indica una opción disponible en el HTML, no un estado operativo comprobado.

### SGC: estado conocido

El HTML contiene un intento de consulta al feed oficial GeoJSON de cinco días del SGC y rutas de respaldo. **La conexión no quedó verificada y no debe considerarse operativa:** en las comprobaciones del 10 de noviembre de 2026, el feed devolvió `403 AccessDenied`, los proxies configurados no ofrecieron un respaldo válido y no se confirmó el FDSN alternativo. El servicio ArcGIS consultado expuso datos del catálogo, pero esas pruebas no demostraron que fuera una fuente adecuada de sismicidad reciente.

Por tanto, este README **no promete que los sismos del visor SGC aparezcan en el monitor**. La vista del SGC puede incluir también eventos de otras agencias; sus datos no deben atribuirse todos al SGC sin comprobar la agencia de cada evento.

### Japón y detección instrumental

- El HTML conserva herramientas de estaciones japonesas y observación instrumental de las fuentes implementadas, así como opciones de métricas.
- Los detectores locales de actividad instrumental son distintos de un catálogo de sismos confirmados y de una alerta oficial. Un grupo de estaciones o un cuadro de movimiento no establece por sí solo un epicentro o una magnitud oficial.
- Una ubicación de catálogo no prueba que la estación transmita en vivo. Las lecturas y métricas solo son actuales cuando llegan tramas válidas y recientes.
- Los cálculos o valores aproximados no deben describirse como mediciones oficiales.

### Taiwán: TREM y P-Alert

El HTML conserva módulos para telemetría/detección instrumental de TREM y P-Alert y sus paneles de métricas. Su disponibilidad depende de sus feeds y del entorno. Movimiento detectado no equivale a un EEW oficial, a Shindo oficial ni a un epicentro confirmado. No se deben completar valores que la fuente no entrega.

### Apartados adicionales

El HTML contiene paneles y controladores para las funciones listadas a continuación; su presencia no garantiza que cada proveedor esté respondiendo:

- Centro meteorológico y consultas del tiempo.
- Alertas meteorológicas JMA y alertas NWS/NOAA de Estados Unidos.
- Tifones y huracanes/ciclones tropicales.
- Avisos y productos de tsunami JMA y NOAA/PTWC/NTWC.
- Volcanes JMA y una vista de volcanes/avisos de Colombia y el Caribe.
- Alertas globales GDACS y panel de clima espacial NOAA/SWPC.
- Módulos de movilidad de Bogotá, incluyendo avisos y enlaces de consulta.
- NDMA Japón y módulos adicionales visibles en el archivo, como SIAT-CT.
- Radar meteorológico RainViewer integrado en los mapas compatibles.

Cada apartado tiene su propia fuente, política de actualización y criterios de apertura. Debe consultarse la hora y el estado que muestre el propio panel.

### Recorrido por apartados

- En Ajustes hay un control **Recorrido por apartados** y un intervalo configurable entre 1 y 60 minutos, con 1 minuto como valor inicial.
- El HTML incluye una lista de apartados para recorrer y una preferencia guardada en el navegador.
- La existencia del control y su código se comprobaron estáticamente, pero **no se probó el recorrido en navegador**. No se garantiza que cada paso abra correctamente ni que todos los temporizadores o avisos automáticos queden suprimidos mientras esté activo.

### Sonidos y voz

- El HTML incluye sonidos de interfaz y de alertas, ajustes de audio y control de volumen.
- También incluye síntesis de voz (`SpeechSynthesis`) para informes sísmicos nuevos que cumplan los criterios del código. El idioma de locución puede variar según la agencia; la voz depende del navegador y de las voces instaladas.
- No se verificó reproducción de sonido ni pronunciación en un dispositivo físico.

## EEW y ondas

Las conexiones y entradas de agencias EEW que se retiraron de esta edición no se deben presentar como fuentes operativas. El HTML puede conservar código o estilos antiguos residuales, por lo que la inspección estática no equivale a una auditoría dinámica exhaustiva de todos los caminos de ejecución. La presencia de funciones TauP o código heredado no demuestra que haya una alerta EEW conectada o vigente.

## Uso responsable y limitaciones

- Este HTML es una herramienta informativa; no sustituye a las agencias ni a las instrucciones de protección civil.
- Distingue sismos de catálogo, reportes preliminares, detección instrumental y estimaciones. No infieras una medición oficial a partir de una aproximación o de datos ausentes.
- CORS, proxies, endpoints, permisos del navegador, servicios de mapas y redes móviles pueden bloquear o retrasar consultas.
- Revisa la fuente y la hora del dato antes de tomar decisiones; no uses el indicador de conexión como confirmación de telemetría reciente si no hay una lectura válida.

## Licencias y atribución

- Los metadatos del HTML declaran **AGPL-3.0-or-later** y reconocen componentes derivados/adaptados de SesnaQuake. Antes de redistribuir una versión modificada, revisa y cumple la licencia y las atribuciones que correspondan.
- Los sonidos, mapas, bibliotecas, datos y servicios externos pueden tener licencias y términos independientes. Consulta las condiciones de cada proveedor antes de reutilizarlos.
