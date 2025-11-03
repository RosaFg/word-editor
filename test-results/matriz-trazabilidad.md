Matriz de Trazabilidad - Editor Word Masivo
Informacion del Documento
Proyecto: Editor Word Masivo v1.0
Documento: Matriz de Trazabilidad
Version: 1.0
Fecha: 22/10/2025
Preparado por: Rosa QA
Estado: Completo

1. Introduccion
1.1 Proposito
Esta matriz establece la trazabilidad entre requisitos funcionales, casos de prueba ejecutados, defectos encontrados y resultados obtenidos, asegurando que todos los requisitos han sido verificados.
1.2 Alcance
Cubre todos los requisitos funcionales del Editor Word Masivo v1.0 y su validacion mediante casos de prueba.

2. Matriz de Trazabilidad Completa
RF-001: Cargar un solo archivo Word (.docx)

Prioridad: Alta
Casos de Prueba: TC-001
Estado TC: PASS
Bugs Relacionados: Ninguno
Cobertura: 100%

RF-002: Cargar multiples archivos Word

Prioridad: Alta
Casos de Prueba: TC-002
Estado TC: PASS
Bugs Relacionados: Ninguno
Cobertura: 100%

RF-003: Buscar texto con resaltado en tiempo real

Prioridad: Alta
Casos de Prueba: TC-003
Estado TC: PASS
Bugs Relacionados: Ninguno
Cobertura: 100%

RF-004: Reemplazo selectivo de texto (uno por uno)

Prioridad: Alta
Casos de Prueba: TC-004
Estado TC: FAIL
Bugs Relacionados: BUG-001
Cobertura: 100%

RF-005: Reemplazo masivo en todos los documentos

Prioridad: Alta
Casos de Prueba: TC-005
Estado TC: PASS
Bugs Relacionados: Ninguno
Cobertura: 100%

RF-006: Navegar entre multiples documentos

Prioridad: Media
Casos de Prueba: TC-006
Estado TC: PASS
Bugs Relacionados: Ninguno
Cobertura: 100%

RF-007: Deshacer cambios realizados

Prioridad: Media
Casos de Prueba: TC-007
Estado TC: PASS
Bugs Relacionados: BUG-002
Cobertura: 100%

RF-008: Guardar archivos modificados

Prioridad: Alta
Casos de Prueba: TC-008
Estado TC: PASS
Bugs Relacionados: Ninguno
Cobertura: 100%

RF-009: Limpiar interfaz (campos y area de texto)

Prioridad: Baja
Casos de Prueba: TC-009
Estado TC: PASS
Bugs Relacionados: Ninguno
Cobertura: 100%

RF-010: Validar y manejar archivos no validos

Prioridad: Media
Casos de Prueba: TC-010
Estado TC: PASS
Bugs Relacionados: Ninguno
Cobertura: 100%


3. Matriz Inversa: Casos de Prueba vs Requisitos
TC-001: Carga Individual

Requisitos Cubiertos: RF-001
Resultado: PASS
Prioridad: Alta

TC-002: Carga Multiple

Requisitos Cubiertos: RF-002
Resultado: PASS
Prioridad: Alta

TC-003: Busqueda y Resaltado

Requisitos Cubiertos: RF-003
Resultado: PASS
Prioridad: Alta

TC-004: Reemplazo Selectivo

Requisitos Cubiertos: RF-004
Resultado: FAIL
Prioridad: Alta

TC-005: Reemplazo Masivo

Requisitos Cubiertos: RF-005
Resultado: PASS
Prioridad: Alta

TC-006: Navegacion Entre Documentos

Requisitos Cubiertos: RF-006
Resultado: PASS
Prioridad: Media

TC-007: Deshacer Cambios

Requisitos Cubiertos: RF-007
Resultado: PASS
Prioridad: Media

TC-008: Guardado de Archivos

Requisitos Cubiertos: RF-008
Resultado: PASS
Prioridad: Alta

TC-009: Limpiar Interfaz

Requisitos Cubiertos: RF-009
Resultado: PASS
Prioridad: Baja

TC-010: Manejo de Errores

Requisitos Cubiertos: RF-010
Resultado: PASS
Prioridad: Media


4. Matriz de Defectos vs Requisitos
BUG-001: Reemplazo selectivo falla con multiples coincidencias

Severidad: Media
Requisito Afectado: RF-004
Caso de Prueba: TC-004
Estado: Abierto
Descripcion: Al usar reemplazo selectivo en un parrafo con multiples coincidencias, solo se aplica correctamente el primer reemplazo

BUG-002: Historial de deshacer confuso al navegar

Severidad: Baja
Requisito Afectado: RF-007
Caso de Prueba: TC-007
Estado: Abierto
Descripcion: Al deshacer cambios despues de navegar entre documentos, no es claro en que documento se deshizo el cambio


5. Estadisticas de Cobertura
5.1 Cobertura de Requisitos
Requisitos Totales: 10 (100%)
Requisitos Cubiertos por TC: 10 (100%)
Requisitos No Cubiertos: 0 (0%)
Requisitos con Defectos: 2 (20%)
Requisitos Sin Defectos: 8 (80%)
5.2 Cobertura por Prioridad
Prioridad Alta:

Total de Requisitos: 6
Cubiertos: 6
Porcentaje: 100%

Prioridad Media:

Total de Requisitos: 3
Cubiertos: 3
Porcentaje: 100%

Prioridad Baja:

Total de Requisitos: 1
Cubiertos: 1
Porcentaje: 100%

5.3 Resultados de Casos de Prueba
PASS: 9 casos (90%)
FAIL: 1 caso (10%)
BLOCKED: 0 casos (0%)
NOT EXECUTED: 0 casos (0%)

6. Analisis de Gaps
6.1 Requisitos Sin Cobertura
Ninguno - Todos los requisitos funcionales tienen al menos un caso de prueba asociado.
6.2 Casos de Prueba Sin Requisito
Ninguno - Todos los casos de prueba estan vinculados a requisitos funcionales.
6.3 Requisitos de Alto Riesgo
RF-004 (Reemplazo Selectivo)

Nivel de Riesgo: Alto
Razon: Defecto conocido BUG-001
Mitigacion: Documentar workaround, usar reemplazo masivo como alternativa

RF-008 (Guardado de Archivos)

Nivel de Riesgo: Medio
Razon: Funcion critica sin validacion de sobrescritura
Mitigacion: Recomendar guardar en carpeta diferente a la original


7. Matriz de Trazabilidad Bidireccional
RF-001 - TC-001 - PASS
Requisito: Cargar archivo individual
Caso de Prueba: Verificar carga individual
Resultado: PASS
Defectos: Ninguno
RF-002 - TC-002 - PASS
Requisito: Cargar archivos multiples
Caso de Prueba: Verificar carga multiple
Resultado: PASS
Defectos: Ninguno
RF-003 - TC-003 - PASS
Requisito: Busqueda con resaltado
Caso de Prueba: Verificar busqueda
Resultado: PASS
Defectos: Ninguno
RF-004 - TC-004 - FAIL
Requisito: Reemplazo selectivo
Caso de Prueba: Verificar reemplazo selectivo
Resultado: FAIL
Defectos: BUG-001 (Severidad Media)
RF-005 - TC-005 - PASS
Requisito: Reemplazo masivo
Caso de Prueba: Verificar reemplazo masivo
Resultado: PASS
Defectos: Ninguno
RF-006 - TC-006 - PASS
Requisito: Navegacion entre documentos
Caso de Prueba: Verificar navegacion
Resultado: PASS
Defectos: Ninguno
RF-007 - TC-007 - PASS
Requisito: Deshacer cambios
Caso de Prueba: Verificar deshacer
Resultado: PASS
Defectos: BUG-002 (Severidad Baja)
RF-008 - TC-008 - PASS
Requisito: Guardar archivos
Caso de Prueba: Verificar guardado
Resultado: PASS
Defectos: Ninguno
RF-009 - TC-009 - PASS
Requisito: Limpiar interfaz
Caso de Prueba: Verificar limpieza
Resultado: PASS
Defectos: Ninguno
RF-010 - TC-010 - PASS
Requisito: Manejo de errores
Caso de Prueba: Verificar validacion
Resultado: PASS
Defectos: Ninguno

8. Matriz de Impacto de Defectos
BUG-001: Impacto en Reemplazo Selectivo

Requisitos Impactados: RF-004
Casos de Prueba Afectados: TC-004
Funcionalidades Alternativas: Usar reemplazo masivo (RF-005, TC-005)
Workaround: Usar boton "Reemplazar Todo" que funciona correctamente

BUG-002: Impacto en Historial de Deshacer

Requisitos Impactados: RF-007
Casos de Prueba Afectados: TC-007
Funcionalidades Alternativas: Evitar navegar entre documentos antes de deshacer
Workaround: Deshacer inmediatamente despues de cada cambio, antes de navegar


9. Recomendaciones
9.1 Para Desarrollo

Prioridad Alta: Corregir BUG-001 - Afecta funcionalidad principal de reemplazo selectivo
Revisar logica de indices en la funcion replace_text_selective
Considerar implementar historial por documento en lugar de global

9.2 Para Testing

Agregar casos de prueba de regresion para BUG-001 despues de correccion
Crear casos adicionales para pruebas de rendimiento con archivos grandes
Expandir TC-010 con mas tipos de archivos invalidos y casos limite

9.3 Para Documentacion

Actualizar manual de usuario con limitaciones conocidas
Documentar workarounds para BUG-001 y BUG-002
Agregar seccion de FAQ sobre uso correcto del reemplazo selectivo


10. Historial de Cambios
Version 1.0 - 22/10/2025

Creacion inicial de la matriz de trazabilidad
Documentacion de 10 requisitos funcionales
Vinculacion con 10 casos de prueba
Documentacion de 2 defectos encontrados
Autor: Rosa QA
