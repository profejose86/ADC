# Revisión del Asistente Docente Chaco, versión 60

Fecha de revisión: 11 de noviembre de 2026.

Archivo revisado: `Asistente_Docente_Chaco_v0_9_16_60.html`.

## Alcance y evidencia

Revisión de solo lectura del HTML y de las dos conversaciones compartidas por el usuario. Se cotejaron los pedidos visibles en esas copias con la implementación actual. Las copias incluyen imágenes y archivos adjuntos cuyo contenido completo no se inspeccionó. Por ello, este informe no certifica haber recuperado cada pedido de toda la historia del proyecto.

Se comprobaron sintácticamente 19 bloques JavaScript mediante el compilador de Node, sin errores. Esto verifica sintaxis, pero no ejecución, cálculos ni interacción con el DOM.

La herramienta de Chrome rechazó la navegación al archivo local por su política de protocolos. La captura de pantalla de aplicaciones externas tampoco está disponible en este dispositivo. No se realizaron pruebas interactivas, impresión real ni evaluación visual directa. Los estados siguientes describen evidencia del código, salvo indicación expresa.

## Resultado general

La versión contiene un flujo amplio de perfil docente, instituciones y cargos, solicitudes DL-01, declaraciones DJ-01 y DJ-02, OL-01, calendario y editor de diseño. Las últimas propuestas de convertir el editor en un lienzo libre están implementadas parcialmente. No hay evidencia suficiente para afirmar que todas las funciones operen correctamente en navegador.

## Pedidos e implementación

| Pedido recuperado | Evidencia en la versión 60 | Evaluación |
| --- | --- | --- |
| Separar apellidos, nombres y DNI | Campos de perfil y sincronización con formularios | Presente. Falta comprobar la disposición visual de los tres campos y datos antiguos. |
| DJ-02 manipulable | Tabla HTML, celdas y controles de edición | Presente. No se reduce a una imagen fija. La fidelidad respecto de los PDF adjuntos requiere comparación visual. |
| Nombres alineados a la izquierda y en negrita | Renderizado y ajuste de campos personales | Revisar visualmente todos los campos y la impresión. No se certifica la alineación final. |
| Letras ajustadas a los recuadros | `fitAll`, medición con canvas y tamaños mínimos | Presente en un renderizador anterior. El renderizador final vuelve a construir la tabla. Hay que verificar el alcance efectivo de ese ajuste en la vista final. |
| Pendientes DL-01 dentro del DJ-02 | Migración y registro `adc58`, estados pending/granted/deleted | Presente. Las pendientes se muestran en edición. |
| Confirmar licencia desde su fila | Acción Licencia otorgada y validación de campos/fechas | Presente. Confirmar con datos válidos e inválidos sigue pendiente de prueba. |
| Eliminar, deshacer y restaurar | Estado anterior conservado, sección Licencias eliminadas | Presente. Restaurar recupera otorgada o pendiente según el estado previo. |
| Reimprimir sin duplicar ni revivir eliminadas | Firma por DNI, motivo y período, registro de filas fuente | Protección explícita. Requiere pruebas con varias instituciones y solicitudes distintas del mismo período. |
| Excluir inasistencias justificadas del DJ-02 | Filtro al migrar pendientes, proyectar e imprimir | Presente. Verificar variantes históricas de nomenclatura. |
| Carga manual de antecedentes | Creación de licencia manual | Presente. La nueva licencia comienza pendiente y necesita confirmación, incluso si se carga como antecedente ya otorgado. |
| Imprimir solamente otorgadas | Vista de impresión filtra por estado y valida datos | Presente. Falta comprobar PDF, saltos de página y retorno tras cancelar impresión. |
| Filas vacías de altura razonable | Altura mediana de las filas ocupadas | Presente. Paginación con espacio estimado de 442 píxeles. |
| Acciones que acompañen cada fila con zoom | Botones insertados dentro de la fila | Presente estructuralmente. Verificar legibilidad y espacio con zoom. |
| Tuerquita arrastrable | Eventos de puntero, umbral de 5 píxeles y posición persistida | Presente. El arrastre requiere Ajustes abierto. |
| Tira flotante de herramientas | Panel flotante de hasta 365 píxeles de ancho | Parcial. Continúa siendo un panel con varias filas, no la tira compacta propuesta. |
| Notas, rectángulos y óvalos | Operación annotation y color elegible | Presente. El dibujo queda limitado al contenedor anfitrión. |
| Anotar libremente sobre toda la pantalla | Restricción de dibujo dentro del área elegida | Parcial. Puede impedir atravesar columnas o límites de secciones. |
| Mantener anotaciones al cerrar Ajustes | CSS las muestra solo con adcDesignActive | Pendiente. Al cerrar Ajustes desaparecen. |
| Clic derecho para editar, eliminar y mover | Menú de tres acciones | Presente para elementos elegibles. No cubre indiscriminadamente todo nodo del HTML. |
| Mover y ajustar tamaño con la misma herramienta | Arrastre interior y bordes de tamaño | Presente. Revisar controles protegidos y selección de elementos originales. |
| Seleccionar sin mover accidentalmente | Arranque de arrastre del elemento en pointerdown | Riesgo. El umbral de la tuerquita no demuestra un umbral equivalente para todos los elementos. |
| Doble clic para renombrar | Se encontró doble clic para restablecer área de hoja | El gesto general de doble clic para editar botones y cajas no se encontró. La edición existe mediante panel/menú. |
| Crear cajas y botones | Operaciones box y button | Presente. Los botones nuevos pueden quedar sin acción y se identifican como tales. |
| Eliminar originales de forma reversible | hideOriginal y Deshacer | Presente. Un control oculto puede dificultar completar el trámite hasta recuperarlo. |
| Desplegables automáticos | Cálculo de dirección y creación de panel | Parcial. La elección Auto se resuelve a una dirección al crear. Verificar adaptación posterior al mover o cambiar tamaño de ventana. |
| Deshacer y rehacer | Pila de operaciones y reversas | Presente. Rehacer descarta la operación si no puede aplicarla. Revisar consistencia en ese caso. |
| Exportar e importar distribución | JSON con esquema y validación, rollback de importación | Presente. Hay límites de tamaño y cantidad de operaciones. |
| Guardar borrador | Guardado explícito en localStorage | Presente. Los cambios de diseño requieren guardar o exportar para conservarlos. |
| Nuevo lienzo desde cero | No se encontró acción correspondiente | Pendiente. Nueva sección permite ampliar la página existente. |
| Duplicar y alinear varios elementos | Centrados por referencia disponibles | Parcial. No se encontró duplicado general ni selección múltiple para alineación colectiva. |
| OL-01 con escuelas del perfil | adcOLStart carga instituciones y change actualiza cargos | Presente. Hay un retorno temprano al reabrir el mismo borrador que merece comprobarse tras modificar instituciones. |
| Zoom de hoja completa en OL-01 | Zoom aplicado al contenedor del papel, rango 45–110 % | Presente. Validación visual y de impresión pendiente. |

## Hallazgos y riesgos concretos

1. **Restablecer zoom tiene la misma lógica que Ajustar al ancho.** Ambos botones dejan la escala en null y llaman al mismo ajuste. Si Restablecer debe significar 100 %, el comportamiento actual no expresa esa distinción.
2. **La altura del DJ-02 es estimada.** El cálculo usa cantidad de caracteres y limita la fila a 112 píxeles. Textos muy extensos, palabras largas, fuentes o anchos modificados pueden exceder esa estimación. Debe verificarse desbordamiento y paginación con medición real.
3. **Licencias vinculadas comparten estado.** Eliminar o confirmar una licencia modifica todas sus instituciones. Hay aviso explícito, pero puede sorprender si se actúa desde un filtro por escuela.
4. **La identidad de una licencia usa DNI, motivo y período.** Agrupa solicitudes coincidentes. Dos solicitudes independientes con esos mismos valores podrían unificarse. La decisión funcional requiere casos reales.
5. **Los antecedentes manuales arrancan pendientes.** Esto añade una confirmación a una licencia histórica ya otorgada. Conviene aclararlo en el flujo y verificar que la persona entienda por qué aún no aparece al imprimir.
6. **Datos guardados por navegador y origen.** Perfil, licencias y diseño usan localStorage. La copia local y la página de GitHub tienen almacenamientos distintos. El traslado de datos debe probarse mediante exportación e importación.
7. **El editor aplica operaciones sobre elementos identificados.** Cambios estructurales de futuras versiones pueden volver incompatible un borrador. La importación ya intenta revertir fallos, pero conviene probar migraciones representativas.
8. **Hay renderizadores y funciones reemplazados posteriormente.** DJ-02 acumula implementaciones anteriores y una capa final que sobrescribe funciones. Leer una función anterior no basta para demostrar el comportamiento vigente. Esto aumenta el costo de mantenimiento y el riesgo de regresión.
9. **La edición exige descubrir herramientas y diálogos.** El panel contiene muchas acciones y utiliza prompts para varias entradas. La amplitud de funciones puede resultar difícil para usuarios sin experiencia.

## Sugerencias de experiencia de uso

- Dar prioridad a seleccionar, mover, ajustar tamaño y editar texto dentro de una selección persistente.
- Mostrar una tira compacta con herramientas frecuentes y un acceso claro a opciones avanzadas.
- Incorporar Mantener anotaciones visibles con controles inferiores operables al cerrar el editor.
- Definir claramente qué pertenece al formulario, qué es una anotación y qué se guarda en cada exportación.
- Mostrar el estado de guardado y facilitar la recuperación de borradores.
- Explicar en el propio botón o confirmación cuándo una acción afecta a varias instituciones.
- Mantener estados Pendiente, Otorgada y Eliminada con texto legible y mensajes breves de resultado.
- Sustituir los diálogos de texto libre por formularios visibles donde haya opciones conocidas.
- Evaluar contraste, foco de teclado, tamaño de controles, pantallas pequeñas y zoom antes de certificar una apariencia profesional.
- Reservar el informe visual definitivo hasta observar la aplicación renderizada y su impresión.

## Pruebas que faltan para cerrar la validación funcional

1. Cargar un perfil nuevo y otro guardado anteriormente, comprobar nombres, DNI, escuelas, cargos y horarios.
2. Generar DL-01 dos veces, comprobar una sola licencia, confirmar y revisar vista imprimible.
3. Eliminar y restaurar pendientes y otorgadas, regenerar una eliminada y comprobar que continúa eliminada.
4. Repetir con una licencia vinculada a dos instituciones y con filtros por escuela.
5. Crear antecedente manual, confirmar, guardar, recargar y comprobar persistencia.
6. Introducir fechas inválidas, datos incompletos e inasistencias justificadas.
7. Probar tablas vacías, textos muy largos y varias páginas, exportar a PDF y comparar con los formularios de referencia.
8. Arrastrar la tuerquita a los cuatro bordes, cambiar tamaño de ventana y recargar.
9. Crear nota, recuadro, óvalo, caja, botón y desplegable, mover y redimensionar cada uno, editar y deshacer.
10. Renombrar un botón original y comprobar que conserva su acción. Ocultarlo y recuperarlo.
11. Exportar borrador, importar el mismo, intentar uno inválido y comprobar recuperación del diseño previo.
12. Probar el selector del OL-01, modificar instituciones en el perfil, volver al borrador y verificar actualización.
13. Probar zoom mínimo, máximo, Ajustar al ancho y Restablecer, además de la impresión.
14. Verificar teclado, foco, móvil, contraste, legibilidad y cantidad de pasos para un docente sin experiencia.

## Cierre de esta revisión

El informe identifica funciones presentes, cumplimiento parcial y verificaciones pendientes. No certifica funcionamiento visual ni normativo. La sintaxis JavaScript pasó. No se modificó el HTML, no se publicaron cambios ni se convirtió esta lista en una implementación. Los pendientes quedan documentados para que el usuario decida posteriormente las actividades por realizar.
