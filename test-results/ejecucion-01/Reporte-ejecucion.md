Reporte de Ejecucion - Ciclo 01
Informacion del Documento
Proyecto: Editor Word Masivo v1.0
Documento: Reporte de Ejecucion de Pruebas
Ciclo: Ejecucion 01
Version Build: v1.0
Fecha Inicio: 22/10/2025
Fecha Fin: 22/10/2025
Ejecutado por: Rosa QA

1. Resumen Ejecutivo
1.1 Objetivo del Ciclo
Ejecutar el conjunto completo de casos de prueba (TC-001 a TC-010) para validar las funcionalidades principales del Editor Word Masivo v1.0 y verificar el cumplimiento de requisitos funcionales.
1.2 Resultados Generales
Casos Planificados: 10
Casos Ejecutados: 10
Casos Exitosos (PASS): 9
Casos Fallidos (FAIL): 1
Casos Bloqueados: 0
Tasa de Exito: 90%
Defectos Encontrados: 2
Defectos Criticos: 0
Cobertura Alcanzada: 100%
1.3 Veredicto
APROBADO CON OBSERVACIONES
La aplicacion cumple con el 90% de los casos de prueba. Los 2 defectos encontrados son de severidad Media y Baja, con workarounds disponibles. Se recomienda proceder al release documentando las limitaciones conocidas.

2. Detalles de Ejecucion por Caso de Prueba
2.1 Resumen de Ejecucion
TC-001: Carga Individual

Prioridad: Alta
Resultado: PASS
Tiempo: 3 minutos
Defectos: Ninguno
Notas: Funciona correctamente

TC-002: Carga Multiple

Prioridad: Alta
Resultado: PASS
Tiempo: 5 minutos
Defectos: Ninguno
Notas: Probado con 3 archivos

TC-003: Busqueda Texto

Prioridad: Alta
Resultado: PASS
Tiempo: 4 minutos
Defectos: Ninguno
Notas: Resaltado correcto

TC-004: Reemplazo Selectivo

Prioridad: Alta
Resultado: FAIL
Tiempo: 5 minutos
Defectos: BUG-001
Notas: Falla con multiples coincidencias

TC-005: Reemplazo Masivo

Prioridad: Alta
Resultado: PASS
Tiempo: 4 minutos
Defectos: Ninguno
Notas: Funciona en todos los documentos

TC-006: Navegacion

Prioridad: Media
Resultado: PASS
Tiempo: 3 minutos
Defectos: Ninguno
Notas: Botones funcionan correctamente

TC-007: Deshacer

Prioridad: Media
Resultado: PASS
Tiempo: 3 minutos
Defectos: BUG-002
Notas: Funciona pero UX confusa

TC-008: Guardado

Prioridad: Alta
Resultado: PASS
Tiempo: 4 minutos
Defectos: Ninguno
Notas: Archivos guardados correctamente

TC-009: Limpiar

Prioridad: Baja
Resultado: PASS
Tiempo: 2 minutos
Defectos: Ninguno
Notas: Limpia correctamente

TC-010: Manejo Errores

Prioridad: Media
Resultado: PASS
Tiempo: 6 minutos
Defectos: Ninguno
Notas: Valida correctamente

Tiempo Total de Ejecucion: 39 minutos

2.2 Casos Exitosos (PASS)
TC-001: Carga Individual de Archivo
Resultado: PASS
Evidencias: screenshot-tc001-01.png, screenshot-tc001-02.png
Observaciones: El archivo se cargo completamente sin errores. Los acentos y caracteres especiales se mostraron correctamente. La etiqueta se actualizo con el formato esperado "Archivo 1/1: documento-prueba.docx".
TC-002: Carga Multiple de Archivos
Resultado: PASS
Evidencias: screenshot-tc002-01.png, video-tc002.mp4
Observaciones: Los 3 archivos se cargaron en orden correcto. La navegacion funciono perfectamente sin mezclar contenidos entre documentos. Los botones de navegacion se habilitaron correctamente.
TC-003: Busqueda y Resaltado
Resultado: PASS
Evidencias: screenshot-tc003-01.png, screenshot-tc003-02.png
Observaciones: El resaltado aparece instantaneamente mientras se escribe. La busqueda es case-insensitive como se esperaba. Se probaron palabras con acentos y funcionaron correctamente.
TC-005: Reemplazo Masivo
Resultado: PASS
Evidencias: screenshot-tc005-01.png, screenshot-tc005-02.png
Observaciones: Reemplazo correctamente 3 coincidencias en 2 documentos diferentes. El mensaje mostro el conteo correcto de reemplazos realizados. Los cambios persistieron al navegar entre documentos.
TC-006: Navegacion Entre Documentos
Resultado: PASS
Evidencias: video-tc006.mp4
Observaciones: La navegacion respeto los limites correctamente. No fue posible avanzar mas alla del ultimo documento ni retroceder antes del primero. La etiqueta siempre mostro informacion precisa.
TC-007: Funcion Deshacer
Resultado: PASS
Evidencias: screenshot-tc007-01.png, screenshot-tc007-02.png
Observaciones: Deshizo correctamente el cambio realizado. El texto se restauro al estado anterior. Sin embargo, se encontro BUG-002 relacionado con la confusion al navegar entre documentos despues de deshacer.
TC-008: Guardado de Archivos
Resultado: PASS
Evidencias: screenshot-tc008-01.png, screenshot-tc008-02.png, screenshot-tc008-03.png
Observaciones: Los archivos se guardaron correctamente en la carpeta seleccionada. Los archivos pudieron abrirse en Microsoft Word sin problemas. Los cambios realizados persistieron correctamente en los archivos guardados.
TC-009: Limpiar Interfaz
Resultado: PASS
Evidencias: screenshot-tc009-01.png, screenshot-tc009-02.png
Observaciones: Limpio correctamente todos los campos y el area de texto. Los resaltados desaparecieron. Los archivos permanecieron en memoria y el contenido pudo recuperarse navegando entre documentos.
TC-010: Manejo de Errores
Resultado: PASS
Evidencias: screenshot-tc010-01.png, screenshot-tc010-02.png, screenshot-tc010-03.png
Observaciones: Rechazo correctamente archivos .doc, .pdf y .txt. Manejo apropiadamente un archivo corrupto sin causar crash. Los mensajes de error fueron claros y comprensibles para el usuario.

2.3 Casos Fallidos (FAIL)
TC-004: Reemplazo Selectivo
Resultado: FAIL
Defecto: BUG-001
Severidad: Media
Evidencias: screenshot-tc004-fail.png, video-tc004-bug.mp4
Descripcion del Fallo:
Al ejecutar el reemplazo selectivo en un documento con 4 coincidencias de la palabra "cliente" en el mismo parrafo, solo se aplico correctamente el primer reemplazo. Los siguientes reemplazos confirmados no se ejecutaron o reemplazaron texto incorrecto.
Pasos Ejecutados:

Se cargo documento con texto que contenia multiples apariciones de "cliente" en un solo parrafo
Se busco: "cliente"
Se ingreso en reemplazo: "comprador"
Se hizo clic en "Reemplazar" (selectivo)
Se acepto con "Si" para todas las coincidencias
Resultado: Solo el primer "cliente" se reemplazo por "comprador"

Impacto:

Funcionalidad principal afectada
Usuario debe usar reemplazo masivo como alternativa
No causa perdida de datos

Workaround:
Usar la funcion "Reemplazar Todo" (TC-005) que funciona correctamente y reemplaza todas las coincidencias sin problemas.

3. Defectos Encontrados
3.1 Resumen de Defectos
Total de Defectos: 2
Defectos Criticos: 0
Defectos Altos: 0
Defectos Medios: 1
Defectos Bajos: 1
3.2 Distribucion por Severidad
Severidad Critica: 0 defectos (0%)
Severidad Alta: 0 defectos (0%)
Severidad Media: 1 defecto (50%)
Severidad Baja: 1 defecto (50%)
3.3 Defectos Detallados
BUG-001: Reemplazo Selectivo con Multiples Coincidencias

Severidad: Media
Estado: Abierto
Caso de Prueba: TC-004
Descripcion: Al usar reemplazo selectivo en un parrafo con multiples coincidencias, solo se aplica correctamente el primer reemplazo
Workaround: Usar funcion "Reemplazar Todo"
Documentacion Completa: Ver /bug-reports/BUG-001-error-reemplazo-selectivo.md

BUG-002: Historial de Deshacer Confuso con Navegacion

Severidad: Baja
Estado: Abierto
Caso de Prueba: TC-007
Descripcion: Al deshacer cambios despues de navegar entre documentos, no es claro en que documento se deshizo el cambio
Workaround: Evitar navegar entre documentos antes de deshacer
Documentacion Completa: Ver /bug-reports/BUG-002-historial-deshacer-navegacion.md


4. Analisis de Resultados
4.1 Cobertura de Pruebas por Modulo
Modulo: Gestion de Archivos

Total de Casos: 2
Ejecutados: 2
PASS: 2
FAIL: 0
Cobertura: 100%

Modulo: Busqueda

Total de Casos: 1
Ejecutados: 1
PASS: 1
FAIL: 0
Cobertura: 100%

Modulo: Reemplazo

Total de Casos: 2
Ejecutados: 2
PASS: 1
FAIL: 1
Cobertura: 100%

Modulo: Navegacion

Total de Casos: 1
Ejecutados: 1
PASS: 1
FAIL: 0
Cobertura: 100%

Modulo: Historial

Total de Casos: 1
Ejecutados: 1
PASS: 1
FAIL: 0
Cobertura: 100%

Modulo: Guardado

Total de Casos: 1
Ejecutados: 1
PASS: 1
FAIL: 0
Cobertura: 100%

Modulo: Interfaz de Usuario

Total de Casos: 1
Ejecutados: 1
PASS: 1
FAIL: 0
Cobertura: 100%

Modulo: Validacion

Total de Casos: 1
Ejecutados: 1
PASS: 1
FAIL: 0
Cobertura: 100%

TOTAL:

Total de Casos: 10
Ejecutados: 10
PASS: 9
FAIL: 1
Cobertura: 100%

4.2 Cobertura por Prioridad
Prioridad Alta:

Total: 6 casos
PASS: 5 casos
FAIL: 1 caso
Porcentaje de Exito: 83%

Prioridad Media:

Total: 3 casos
PASS: 3 casos
FAIL: 0 casos
Porcentaje de Exito: 100%

Prioridad Baja:

Total: 1 caso
PASS: 1 caso
FAIL: 0 casos
Porcentaje de Exito: 100%

4.3 Tendencias y Observaciones
Observaciones Positivas:

El 90% de casos pasaron exitosamente
Todos los casos de prioridad Media y Baja pasaron sin problemas
No se encontraron defectos criticos que bloqueen el release
La aplicacion demostro estabilidad sin crashes
Buen manejo de errores y validacion de entradas

Areas de Atencion:

Solo 1 fallo en funcionalidad principal (Alta prioridad)
El modulo de Reemplazo tiene el 50% de casos fallidos
Se requiere correccion del BUG-001 para proxima version



5. Ambiente de Pruebas
5.1 Configuracion de Hardware
Procesador: Intel Core i5-10400
RAM: 16 GB DDR4
Disco: SSD 512 GB
Monitor: 1920x1080 Full HD
5.2 Configuracion de Software
Sistema Operativo: Windows 11 Pro 64-bit
Aplicacion Bajo Prueba: Editor Word Masivo v1.0 (.exe)
Microsoft Word: Office 2021
Herramienta Screenshots: ShareX 14.1.0
Herramienta Videos: OBS Studio 29.0
5.3 Datos de Prueba
Ubicacion: C:\test-data\
Archivos Word Utilizados: 15 archivos .docx
Archivos Invalidos: 3 archivos (.doc, .pdf, corrupto.docx)
Tamaño Total: Aproximadamente 2.5 MB

6. Lecciones Aprendidas
6.1 Lo que Funciono Bien

La preparacion de datos de prueba fue exhaustiva y cubrio todos los escenarios
Los casos de prueba estaban bien documentados con pasos claros
Las evidencias se capturaron sistematicamente durante toda la ejecucion
La ejecucion fue fluida sin interrupciones tecnicas
