# TC-001: Verificar Carga Individual de Archivo Word

## Información General
- **ID**: TC-001
- **Módulo**: Gestión de Archivos
- **Prioridad**: Alta
- **Tipo**: Funcional - Positiva
- **Fecha Creación**: 22/10/2025
- **Creado por**: Rosa QA
- **Última Actualización**: 22/10/2025
- **Estado**: Activo


## Objetivo
Verificar que la aplicación puede cargar correctamente un único archivo `.docx` y mostrar su contenido completo en el área de texto sin pérdida de información.

## Precondiciones
- [ ] La aplicación Editor Word Masivo está instalada y funcional
- [ ] Existe al menos un archivo `.docx` válido disponible para la prueba
- [ ] El usuario tiene permisos de lectura sobre el archivo de prueba
- [ ] El archivo de prueba no está abierto en otra aplicación
- [ ] La aplicación no tiene archivos previamente cargados

## Datos de Prueba

| Campo | Valor |
|-------|-------|
| **Nombre del archivo** | documento-prueba.docx |
| **Ubicación** | C:\test-data\ |
| **Tamaño** | 15 KB (aproximado) |
| **Número de párrafos** | 5 |
| **Contenido** | Texto simple en español con acentos |
| **Formato original** | Texto plano, sin tablas ni imágenes |

**Contenido de ejemplo del archivo:**
```
Este es el primer párrafo del documento de prueba.

El cliente visitó la tienda ayer.

Los productos incluyen: computadoras, teléfonos y accesorios.

El precio total es $1,500.00 pesos.

Fin del documento.
```

## Pasos de Ejecución

| Paso | Acción | Datos de Entrada | Resultado Esperado |
|------|--------|------------------|-------------------|
| 1 | Ejecutar la aplicación haciendo doble clic en EditorWordMasivo.exe | - | La ventana de la aplicación se abre con dimensiones 900x600. Se muestra la interfaz con todos los botones y campos |
| 2 | Verificar estado inicial de la interfaz | - | El área de texto está vacía. La etiqueta inferior muestra "No hay archivos cargados" |
| 3 | Hacer clic en el botón "Cargar Word" | - | Se abre el diálogo de selección de archivos del sistema operativo |
| 4 | Navegar hasta la ubicación del archivo | C:\test-data\ | La carpeta se abre y muestra los archivos disponibles |
| 5 | Seleccionar el archivo "documento-prueba.docx" | documento-prueba.docx | El archivo aparece seleccionado en el diálogo (resaltado en azul) |
| 6 | Hacer clic en el botón "Abrir" del diálogo | - | El diálogo se cierra |
| 7 | Observar el área de texto de la aplicación | - | El contenido del documento aparece en el área de texto |
| 8 | Verificar la etiqueta de archivo en la parte inferior | - | La etiqueta muestra: "Archivo 1/1: documento-prueba.docx" |
| 9 | Verificar que cada párrafo está presente | - | Los 5 párrafos son visibles en el área de texto |
| 10 | Verificar los saltos de línea entre párrafos | - | Existen dos saltos de línea entre cada párrafo |
| 11 | Hacer scroll en el área de texto | - | El scroll funciona correctamente si el contenido excede el área visible |
| 12 | Verificar caracteres especiales | - | Los acentos, ñ, signos de puntuación y símbolos ($) se muestran correctamente |


## Resultado Esperado

### Resultado Principal
El archivo `.docx` se carga completamente sin errores y su contenido de texto plano se muestra en el área de texto de la aplicación.

### Criterios de Aceptación
1. **Carga exitosa**: El archivo se carga sin mensajes de error
2. **Contenido completo**: Todo el texto del documento es visible
3. **Preservación de texto**: No hay pérdida de caracteres o palabras
4. **Estructura**: Los saltos de línea y párrafos se mantienen
5. **Caracteres especiales**: Acentos, ñ y símbolos se muestran correctamente
6. **Etiqueta actualizada**: Muestra "Archivo 1/1: [nombre-archivo].docx"
7. **Sin mensajes de error**: No aparecen messageboxes de error

### Datos Específicos Esperados
- Texto visible: Todo el contenido del archivo
- Número de líneas visibles: Corresponde al número de párrafos + líneas en blanco
- Etiqueta inferior: "Archivo 1/1: documento-prueba.docx"
- Estado de botones: Todos los botones están habilitados excepto navegación (Anterior/Siguiente)


## Postcondiciones
- El archivo queda cargado en la memoria de la aplicación (self.docs)
- La ruta del archivo se almacena en la lista de rutas (self.file_paths)
- El índice actual se establece en 0 (self.current_index = 0)
- El historial se inicializa con el estado del documento (self.history)
- El usuario puede realizar operaciones de búsqueda, reemplazo y guardado
- Los botones "Reemplazar", "Reemplazar Todo", "Deshacer", "Guardar Como" y "Limpiar" quedan habilitados
- Los botones "Anterior" y "Siguiente" permanecen deshabilitados (solo hay 1 archivo)


## Dependencias
- **Requisitos previos**: REQ-001 (Carga de archivos)
- **Casos relacionados**: TC-002 (Carga múltiple), TC-010 (Manejo de errores)
- **Bloquea**: TC-003 (Búsqueda), TC-004 (Reemplazo), TC-008 (Guardado)

## Notas Adicionales
- **Tiempo estimado de ejecución**: 3 minutos
- **Frecuencia de ejecución**: Cada build, pruebas de regresión
- **Variaciones a probar**:
  - Archivos con nombres que incluyen espacios
  - Archivos con nombres que incluyen acentos
  - Archivos en diferentes rutas (Desktop, Documentos, USB)
  - Archivos de diferentes tamaños (pequeños, medianos, grandes)
- **Limitaciones conocidas**: El formato (negrita, cursiva, colores) no se preserva

## Evidencias Requeridas
- [ ] Screenshot del estado inicial (área de texto vacía)
- [ ] Screenshot del diálogo de selección de archivo
- [ ] Screenshot del contenido cargado en el área de texto
- [ ] Screenshot de la etiqueta mostrando "Archivo 1/1: documento-prueba.docx"
- [ ] Screenshot de caracteres especiales correctamente renderizados

## Criterios de Fallo
El caso de prueba **FALLA** si:
- El archivo no se carga (no aparece contenido)
- Se muestra un mensaje de error al cargar
- El contenido se muestra incompleto (faltan párrafos)
- Los caracteres especiales se muestran incorrectamente (símbolos raros)
- La etiqueta no se actualiza o muestra información incorrecta
- El área de texto muestra contenido corrupto o ilegible
- La aplicación se cierra inesperadamente (crash)

## Historial de Ejecuciones

| Fecha | Ejecutado por | Build | Resultado | Defectos Encontrados | Observaciones |
|-------|---------------|-------|-----------|---------------------|---------------|
| 22/10/2025 | Rosa QA | v1.0 | PASS | Ninguno | Funciona correctamente |
| - | - | - | - | - | - |


# TC-002: Verificar Carga Múltiple de Archivos Word

## Objetivo
Verificar que la aplicación puede cargar correctamente múltiples archivos `.docx` simultáneamente y permite la navegación entre ellos manteniendo el contenido de cada uno.


## Precondiciones
- [ ] La aplicación Editor Word Masivo está instalada y funcional
- [ ] Existen al menos 3 archivos `.docx` válidos disponibles
- [ ] El usuario tiene permisos de lectura sobre todos los archivos
- [ ] Los archivos no están abiertos en otras aplicaciones
- [ ] La aplicación no tiene archivos previamente cargados

## Datos de Prueba

| Archivo | Tamaño | Párrafos | Contenido Distintivo |
|---------|--------|----------|---------------------|
| **doc1.docx** | 10 KB | 3 | "Este es el documento UNO" |
| **doc2.docx** | 12 KB | 4 | "Este es el documento DOS" |
| **doc3.docx** | 15 KB | 5 | "Este es el documento TRES" |

**Ubicación**: C:\test-data\

## Pasos de Ejecución

| Paso | Acción | Datos de Entrada | Resultado Esperado |
|------|--------|------------------|-------------------|
| 1 | Ejecutar la aplicación | - | La aplicación se abre correctamente |
| 2 | Verificar estado inicial | - | Área de texto vacía, etiqueta: "No hay archivos cargados" |
| 3 | Hacer clic en "Cargar Varios Word" | - | Se abre el diálogo de selección múltiple |
| 4 | Navegar a C:\test-data\ | - | La carpeta se abre mostrando los 3 archivos |
| 5 | Seleccionar doc1.docx (primer clic) | doc1.docx | El archivo aparece seleccionado |
| 6 | Mantener Ctrl presionado y hacer clic en doc2.docx | Ctrl + doc2.docx | Ambos archivos están seleccionados |
| 7 | Mantener Ctrl presionado y hacer clic en doc3.docx | Ctrl + doc3.docx | Los 3 archivos están seleccionados |
| 8 | Hacer clic en "Abrir" | - | El diálogo se cierra |
| 9 | Verificar contenido mostrado | - | Se muestra el contenido de doc1.docx (primer archivo) |
| 10 | Verificar etiqueta | - | Muestra: "Archivo 1/3: doc1.docx" |
| 11 | Verificar texto distintivo | - | El texto "Este es el documento UNO" es visible |
| 12 | Hacer clic en "Siguiente >>" | - | El contenido cambia al documento 2 |
| 13 | Verificar nuevo contenido | - | Se muestra el contenido de doc2.docx |
| 14 | Verificar etiqueta actualizada | - | Muestra: "Archivo 2/3: doc2.docx" |
| 15 | Verificar texto distintivo | - | El texto "Este es el documento DOS" es visible |
| 16 | Hacer clic en "Siguiente >>" nuevamente | - | El contenido cambia al documento 3 |
| 17 | Verificar contenido doc3 | - | Se muestra el contenido de doc3.docx |
| 18 | Verificar etiqueta | - | Muestra: "Archivo 3/3: doc3.docx" |
| 19 | Verificar texto distintivo | - | El texto "Este es el documento TRES" es visible |
| 20 | Hacer clic en "Siguiente >>" | - | No ocurre cambio (ya está en el último) |
| 21 | Hacer clic en "<< Anterior" | - | Regresa a doc2.docx |
| 22 | Verificar etiqueta | - | Muestra: "Archivo 2/3: doc2.docx" |
| 23 | Hacer clic en "<< Anterior" nuevamente | - | Regresa a doc1.docx |
| 24 | Verificar etiqueta | - | Muestra: "Archivo 1/3: doc1.docx" |
| 25 | Hacer clic en "<< Anterior" | - | No ocurre cambio (ya está en el primero) |

## Resultado Esperado

### Resultado Principal
Los 3 archivos se cargan correctamente y la aplicación permite navegar entre ellos manteniendo el contenido individual de cada documento sin pérdida de datos.

### Criterios de Aceptación
1. **Carga múltiple exitosa**: Los 3 archivos se cargan sin errores
2. **Orden correcto**: Los archivos se cargan en el orden de selección
3. **Navegación funcional**: Los botones Anterior/Siguiente funcionan correctamente
4. **Contenido preservado**: Cada documento mantiene su contenido al navegar
5. **Etiqueta precisa**: Siempre muestra el índice correcto (X/Y)
6. **Límites respetados**: No avanza más allá del último ni retrocede antes del primero
7. **Sin pérdida de datos**: Al volver a un documento, su contenido es el mismo


## Postcondiciones
- Los 3 archivos quedan cargados en memoria
- Se puede navegar libremente entre ellos
- Cada documento mantiene su estado individual
- Los botones de navegación están habilitados
- El usuario puede realizar operaciones en cualquier documento

## Dependencias
- **Requisitos previos**: REQ-001 (Carga de archivos), REQ-005 (Navegación)
- **Casos relacionados**: TC-001 (Carga individual), TC-006 (Navegación)
- **Prerrequisito**: TC-001 debe pasar

## Notas Adicionales
- **Tiempo estimado**: 5 minutos
- **Variaciones**:
  - Cargar 2 archivos (mínimo)
  - Cargar 10 archivos
  - Cargar 20 archivos (probar rendimiento)
- **Limitación**: Rendimiento puede degradarse con 50+ archivos

## Evidencias Requeridas
- [ ] Screenshot de selección múltiple en el diálogo
- [ ] Screenshot de doc1 cargado con etiqueta "Archivo 1/3"
- [ ] Screenshot de doc2 con etiqueta "Archivo 2/3"
- [ ] Screenshot de doc3 con etiqueta "Archivo 3/3"
- [ ] Video corto (30 seg) de navegación entre documentos


## Criterios de Fallo
El caso **FALLA** si:
- No se pueden seleccionar múltiples archivos
- Solo se carga el primer archivo
- La navegación no funciona
- El contenido se mezcla entre documentos
- La etiqueta muestra información incorrecta
- Se pierde contenido al navegar
- Los botones Anterior/Siguiente no responden

## Historial de Ejecuciones

| Fecha | Ejecutado por | Build | Resultado | Defectos | Observaciones |
|-------|---------------|-------|-----------|----------|---------------|
| 22/10/2025 | Rosa QA | v1.0 | PASS | Ninguno | Funciona correctamente con 3 archivos |


# TC-003: Verificar Búsqueda y Resaltado de Texto

## Objetivo
Verificar que la funcionalidad de búsqueda encuentra todas las coincidencias del texto ingresado y las resalta correctamente en color amarillo en tiempo real.

## Precondiciones
- [ ] La aplicación está abierta
- [ ] Hay al menos un archivo Word cargado
- [ ] El documento contiene texto con palabras repetidas
- [ ] El campo de búsqueda está vacío

## Datos de Prueba

**Archivo**: busqueda-test.docx

**Contenido del documento**:
```
El cliente visitó la tienda.
El cliente compró productos.
Los clientes están satisfechos.
El precio para el cliente es justo.
```

**Términos de búsqueda**:
- "cliente" (aparece 3 veces)
- "Cliente" (mayúscula, debe encontrar "cliente")
- "el" (aparece múltiples veces)
- "productos" (aparece 1 vez)
- "xyz" (no existe en el documento)

## Pasos de Ejecución

| Paso | Acción | Datos | Resultado Esperado |
|------|--------|-------|-------------------|
| 1 | Cargar archivo busqueda-test.docx | - | Contenido visible en área de texto |
| 2 | Verificar campo "Buscar..." | - | Campo vacío, sin resaltados en el texto |
| 3 | Hacer clic en campo "Buscar..." | - | Cursor aparece en el campo |
| 4 | Escribir "c" | "c" | Empieza a buscar (puede resaltar parcialmente) |
| 5 | Escribir "l" | "cl" | Resalta coincidencias con "cl" |
| 6 | Escribir completo "cliente" | "cliente" | Se resaltan 3 coincidencias de "cliente" en amarillo |
| 7 | Contar coincidencias resaltadas | - | Exactamente 3 palabras resaltadas |
| 8 | Verificar que "clientes" NO está resaltado | - | La palabra "clientes" no tiene resaltado (solo "cliente" completo) |
| 9 | Borrar el texto (Ctrl+A, Delete) | - | Los resaltados desaparecen inmediatamente |
| 10 | Escribir "Cliente" (con mayúscula) | "Cliente" | Las 3 coincidencias se resaltan (case-insensitive) |
| 11 | Verificar color del resaltado | - | Color amarillo (#FFFF00 o similar) |
| 12 | Borrar y escribir "el" | "el" | Se resaltan todas las apariciones de "el" |
| 13 | Verificar coincidencias en diferentes posiciones | - | Resalta "El" al inicio, "el" en medio, "el" en final |
| 14 | Borrar y escribir "productos" | "productos" | Se resalta 1 coincidencia |
| 15 | Borrar y escribir "xyz" | "xyz" | No se resalta nada (sin coincidencias) |
| 16 | Verificar que no hay mensaje de error | - | No aparece messagebox ni error |

## Resultado Esperado

### Resultado Principal
La búsqueda funciona en tiempo real, resalta todas las coincidencias encontradas en amarillo, y la búsqueda NO distingue entre mayúsculas y minúsculas.

### Criterios de Aceptación
1. **Tiempo real**: El resaltado ocurre mientras se escribe (sin presionar Enter)
2. **Todas las coincidencias**: Encuentra y resalta todas las apariciones
3. **Case-insensitive**: "cliente" y "Cliente" se tratan igual
4. **Color correcto**: Resaltado en amarillo
5. **Actualización dinámica**: Al modificar la búsqueda, actualiza el resaltado
6. **Limpieza**: Al borrar búsqueda, elimina todos los resaltados
7. **Sin errores**: No muestra mensajes cuando no hay coincidencias

## Postcondiciones
- El texto del documento permanece sin cambios
- Los resaltados son temporales (visuales solamente)
- El campo de búsqueda contiene el último término buscado
- No se modifica el archivo en memoria

## Dependencias
- **Prerrequisito**: TC-001 debe pasar (requiere archivo cargado)
- **Casos relacionados**: TC-004 (Reemplazo usa búsqueda)

## Criterios de Fallo
Falla si:
- No resalta coincidencias
- No funciona en tiempo real (requiere Enter)
- Distingue mayúsculas/minúsculas
- Color de resaltado incorrecto
- No encuentra todas las coincidencias
- No limpia resaltados al borrar búsqueda

## Historial de Ejecuciones

| Fecha | Ejecutado por | Build | Resultado | Defectos | Observaciones |
|-------|---------------|-------|-----------|----------|---------------|
| 22/10/2025 | Rosa QA | v1.0 | PASS | Ninguno | Funciona correctamente |


# TC-004: Verificar Reemplazo Selectivo de Texto

## Objetivo
Verificar que la función de reemplazo selectivo permite al usuario confirmar cada reemplazo individualmente y aplica solo los cambios aceptados.

## Precondiciones
- [ ] La aplicación está abierta
- [ ] Hay un archivo Word cargado con texto repetido
- [ ] Los campos de búsqueda y reemplazo están vacíos

## Datos de Prueba

**Archivo**: reemplazo-test.docx

**Contenido**:
```
El cliente visitó la tienda.
El cliente compró productos.
El precio es para el cliente.
```

**Búsqueda**: "cliente"
**Reemplazo**: "comprador"

## Pasos de Ejecución

| Paso | Acción | Datos | Resultado Esperado |
|------|--------|-------|-------------------|
| 1 | Cargar reemplazo-test.docx | - | Contenido visible |
| 2 | En "Buscar..." escribir "cliente" | cliente | 3 coincidencias resaltadas |
| 3 | En "Reemplazar por..." escribir "comprador" | comprador | Texto ingresado en el campo |
| 4 | Hacer clic en botón "Reemplazar" | - | Aparece diálogo: "¿Reemplazar 'cliente' en el párrafo 1?" |
| 5 | Verificar texto del diálogo | - | Muestra claramente qué se va a reemplazar |
| 6 | Hacer clic en "Sí" | - | Se reemplaza primera coincidencia, aparece segundo diálogo |
| 7 | Verificar segundo diálogo | - | Dice: "¿Reemplazar 'cliente' en el párrafo 2?" |
| 8 | Hacer clic en "No" | - | NO se reemplaza, aparece tercer diálogo |
| 9 | Verificar tercer diálogo | - | Dice: "¿Reemplazar 'cliente' en el párrafo 3?" |
| 10 | Hacer clic en "Sí" | - | Se reemplaza tercera coincidencia |
| 11 | Verificar mensaje final | - | Aparece: "Reemplazo selectivo completado" |
| 12 | Hacer clic en "Aceptar" | - | Mensaje se cierra |
| 13 | Revisar texto en área de texto | - | Línea 1: "El comprador visitó..." (reemplazado) |
| 14 | Revisar línea 2 | - | Línea 2: "El cliente compró..." (NO reemplazado) |
| 15 | Revisar línea 3 | - | Línea 3: "...para el comprador" (reemplazado) |


## Resultado Esperado

### Resultado Principal
El reemplazo selectivo funciona correctamente, permitiendo aceptar o rechazar cada coincidencia individualmente, y aplica solo los cambios confirmados.

### Criterios de Aceptación
1. **Confirmación individual**: Pregunta por cada coincidencia
2. **Información clara**: El diálogo muestra qué se va a reemplazar
3. **Respeta decisiones**: Solo reemplaza cuando se hace clic en "Sí"
4. **Mantiene rechazos**: No reemplaza cuando se hace clic en "No"
5. **Actualiza vista**: Los cambios son visibles inmediatamente
6. **Mensaje final**: Confirma que el proceso terminó
7. **Orden correcto**: Procesa las coincidencias en orden de aparición


## Postcondiciones
- El documento en memoria contiene los cambios aceptados
- Los cambios NO aceptados permanecen sin modificar
- El historial de deshacer se actualiza
- El texto modificado se puede guardar
- El archivo original en disco NO se modifica (hasta guardar)


## Dependencias
- **Prerrequisito**: TC-001 (Carga), TC-003 (Búsqueda)
- **Casos relacionados**: TC-005 (Reemplazo masivo), TC-007 (Deshacer)
- **Bug conocido**: BUG-001 (Problema con múltiples coincidencias en mismo párrafo)


## Notas Adicionales
- **Tiempo estimado**: 5 minutos
- **Limitación conocida**: Si hay múltiples coincidencias en el MISMO párrafo, puede fallar (ver BUG-001)
- **Prueba adicional**: Cancelar en medio del proceso


## Evidencias Requeridas
- [ ] Screenshot del diálogo de confirmación
- [ ] Screenshot del texto ANTES del reemplazo
- [ ] Screenshot del texto DESPUÉS con cambios parciales
- [ ] Screenshot del mensaje "Reemplazo selectivo completado"


## Criterios de Fallo
Falla si:
- No pregunta por cada coincidencia
- Reemplaza todo sin confirmar
- No respeta las decisiones del usuario
- Reemplaza coincidencias rechazadas
- No actualiza el área de texto
- No muestra mensaje final
- Genera error o crash

## Historial de Ejecuciones

| Fecha | Ejecutado por | Build | Resultado | Defectos | Observaciones |
|-------|---------------|-------|-----------|----------|---------------|
| 22/10/2025 | Rosa QA | v1.0 | FAIL | BUG-001 | Falla con múltiples coincidencias en mismo párrafo |

# TC-005: Verificar Reemplazo Masivo en Todos los Documentos


## Objetivo
Verificar que la función de reemplazo masivo reemplaza automáticamente todas las coincidencias en todos los documentos cargados sin pedir confirmación individual.

## Precondiciones
- [ ] La aplicación está abierta
- [ ] Hay al menos 2 archivos Word cargados
- [ ] Los documentos contienen texto con coincidencias del término a buscar

## Datos de Prueba

**Archivos cargados**: 2

**doc1.docx**:
```
El precio es $100.
El precio incluye IVA.
```
(2 coincidencias de "precio")

**doc2.docx**:
```
Consulta el precio en la web.
```
(1 coincidencia de "precio")

**Total de coincidencias**: 3

**Búsqueda**: "precio"
**Reemplazo**: "costo"

## Pasos de Ejecución

| Paso | Acción | Datos | Resultado Esperado |
|------|--------|-------|-------------------|
| 1 | Cargar doc1.docx y doc2.docx | - | 2 archivos cargados |
| 2 | Verificar que se muestra doc1 | - | Etiqueta: "Archivo 1/2: doc1.docx" |
| 3 | En "Buscar..." escribir "precio" | precio | Coincidencias resaltadas |
| 4 | En "Reemplazar por..." escribir "costo" | costo | Texto ingresado |
| 5 | Hacer clic en "Reemplazar Todo" | - | NO aparece diálogo de confirmación |
| 6 | Verificar mensaje | - | Aparece: "Se reemplazaron 3 coincidencias en todos los documentos" |
| 7 | Hacer clic en "Aceptar" | - | Mensaje se cierra |
| 8 | Revisar doc1 (documento actual) | - | Ambas apariciones de "precio" cambiaron a "costo" |
| 9 | Hacer clic en "Siguiente >>" | - | Cambia a doc2 |
| 10 | Revisar doc2 | - | "precio" cambió a "costo" |
| 11 | Contar reemplazos totales | - | 3 reemplazos confirmados (2 en doc1, 1 en doc2) |
| 12 | Volver a doc1 con "<< Anterior" | - | Los cambios persisten |

## Resultado Esperado

### Resultado Principal
El reemplazo masivo reemplaza automáticamente todas las coincidencias en todos los documentos cargados sin pedir confirmación, y muestra el conteo total de reemplazos realizados.

### Criterios de Aceptación
1. **Reemplazo automático**: No pide confirmación individual
2. **Todos los documentos**: Procesa todos los archivos cargados
3. **Todas las coincidencias**: Reemplaza cada aparición encontrada
4. **Conteo correcto**: Muestra el número exacto de reemplazos
5. **Persistencia**: Los cambios se mantienen al navegar entre documentos
6. **Actualización visual**: El área de texto se actualiza con los cambios

## Postcondiciones
- Todos los documentos en memoria contienen los cambios
- El historial de deshacer se actualiza
- Los cambios NO se guardan automáticamente en disco
- Los archivos originales permanecen sin modificar


## Dependencias
- **Prerrequisito**: TC-002 (Carga múltiple), TC-003 (Búsqueda)
- **Casos relacionados**: TC-004 (Reemplazo selectivo), TC-007 (Deshacer)


## Notas Adicionales
- **Tiempo estimado**: 4 minutos
- **Prueba adicional**: Usar con 5+ documentos

## Evidencias Requeridas
- [ ] Screenshot del mensaje "Se reemplazaron X coincidencias"
- [ ] Screenshot de doc1 después del reemplazo
- [ ] Screenshot de doc2 después del reemplazo

## Criterios de Fallo
Falla si:
- Pide confirmación individual
- No reemplaza en todos los documentos
- El conteo de reemplazos es incorrecto
- No actualiza el área de texto
- Los cambios no persisten al navegar
- Genera error

## Historial de Ejecuciones

| Fecha | Ejecutado por | Build | Resultado | Defectos | Observaciones |
|-------|---------------|-------|-----------|----------|---------------|
| 22/10/2025 | Rosa QA | v1.0 | PASS | Ninguno | Funciona correctamente |

# TC-006: Verificar Navegación Entre Documentos


## Objetivo
Verificar que los botones de navegación permiten moverse entre documentos cargados y que la información mostrada corresponde al documento actual.

## Precondiciones
- [ ] La aplicación está abierta
- [ ] Hay 3 archivos Word cargados
- [ ] Se muestra el primer documento

## Datos de Prueba

| Archivo | Contenido Distintivo |
|---------|---------------------|
| doc1.docx | "Documento UNO" |
| doc2.docx | "Documento DOS" |
| doc3.docx | "Documento TRES" |

## Pasos de Ejecución

| Paso | Acción | Resultado Esperado |
|------|--------|-------------------|
| 1 | Cargar 3 documentos | Etiqueta: "Archivo 1/3: doc1.docx" |
| 2 | Verificar contenido | Texto "Documento UNO" visible |
| 3 | Intentar clic en "<< Anterior" | No ocurre cambio (ya está en el primero) |
| 4 | Clic en "Siguiente >>" | Cambia a doc2, etiqueta: "Archivo 2/3: doc2.docx" |
| 5 | Verificar contenido | Texto "Documento DOS" visible |
| 6 | Clic en "Siguiente >>" | Cambia a doc3, etiqueta: "Archivo 3/3: doc3.docx" |
| 7 | Verificar contenido | Texto "Documento TRES" visible |
| 8 | Intentar clic en "Siguiente >>" | No ocurre cambio (ya está en el último) |
| 9 | Clic en "<< Anterior" | Regresa a doc2 |
| 10 | Clic en "<< Anterior" | Regresa a doc1 |


## Resultado Esperado

Los botones de navegación funcionan correctamente, respetan los límites (primer/último documento) y la etiqueta siempre muestra la información correcta.

## Postcondiciones
- El usuario puede navegar libremente entre documentos
- Cada documento mantiene su contenido


## Dependencias
- **Prerrequisito**: TC-002 (Carga múltiple)

## Notas Adicionales
- **Tiempo estimado**: 3 minutos

## Evidencias Requeridas
- [ ] Video de navegación completa (ida y vuelta)

## Criterios de Fallo
Falla si:
- Los botones no responden
- La etiqueta no se actualiza
- El contenido no cambia
- No respeta límites

## Historial de Ejecuciones

| Fecha | Ejecutado por | Build | Resultado | Defectos | Observaciones |
|-------|---------------|-------|-----------|----------|---------------|
| 22/10/2025 | Rosa QA | v1.0 | PASS | Ninguno | Funciona correctamente |

# TC-007: Verificar Función Deshacer Cambios

## Objetivo
Verificar que la función "Deshacer" revierte correctamente los cambios realizados por operaciones de reemplazo.

## Precondiciones
- [ ] La aplicación está abierta
- [ ] Hay un archivo Word cargado
- [ ] Se ha realizado al menos un reemplazo


## Datos de Prueba

**Archivo**: deshacer-test.docx

**Contenido original**:
```
El producto cuesta $100.
```

**Operación**: Reemplazar "producto" por "artículo"

---

## Pasos de Ejecución

| Paso | Acción | Resultado Esperado |
|------|--------|-------------------|
| 1 | Cargar deshacer-test.docx | Contenido original visible |
| 2 | Verificar texto | Muestra "El producto cuesta $100." |
| 3 | Buscar "producto" | Resaltado en amarillo |
| 4 | Reemplazar por "artículo" | - |
| 5 | Clic en "Reemplazar Todo" | Texto cambia a "El artículo cuesta $100." |
| 6 | Verificar cambio aplicado | "artículo" visible, "producto" ya no existe |
| 7 | Clic en botón "Deshacer" | Aparece mensaje: "Cambio deshecho" |
| 8 | Clic en "Aceptar" | Mensaje se cierra |
| 9 | Verificar texto restaurado | Texto vuelve a "El producto cuesta $100." |
| 10 | Intentar deshacer nuevamente | Aparece: "No hay cambios para deshacer" |

## Resultado Esperado

La función "Deshacer" revierte correctamente el último cambio realizado y restaura el estado anterior del documento.

## Postcondiciones
- El documento vuelve al estado previo al reemplazo
- El historial se reduce en un nivel
- Se puede volver a realizar el cambio

## Dependencias
- **Prerrequisito**: TC-004 o TC-005 (Reemplazo)
- **Bug relacionado**: BUG-002 (Historial y navegación)

## Notas Adicionales
- **Tiempo estimado**: 3 minutos
- **Prueba adicional**: Deshacer múltiples cambios consecutivos

## Evidencias Requeridas
- [ ] Screenshot ANTES del reemplazo
- [ ] Screenshot DESPUÉS del reemplazo
- [ ] Screenshot DESPUÉS de deshacer
- [ ] Screenshot del mensaje "Cambio deshecho"


## Criterios de Fallo
Falla si:
- No revierte el cambio
- Revierte cambios incorrectos
- No muestra mensaje de confirmación
- Permite deshacer cuando no hay historial

## Historial de Ejecuciones

| Fecha | Ejecutado por | Build | Resultado | Defectos | Observaciones |
|-------|---------------|-------|-----------|----------|---------------|
| 22/10/2025 | Rosa QA | v1.0 | PASS | BUG-002 | Funciona pero confuso con múltiples docs |

# TC-008: Verificar Guardado de Archivos Modificados


## Objetivo
Verificar que la función "Guardar Como" guarda correctamente todos los archivos modificados en la carpeta seleccionada y que los cambios persisten.

## Precondiciones
- [ ] La aplicación está abierta
- [ ] Hay al menos un archivo Word cargado
- [ ] Se han realizado modificaciones en el documento
- [ ] Existe una carpeta de destino disponible

## Datos de Prueba

**Archivo original**: guardar-test.docx
**Ubicación original**: C:\test-data\
**Contenido original**: "Este es el texto original."
**Modificación**: Reemplazar "original" por "modificado"
**Carpeta destino**: C:\test-results\

## Pasos de Ejecución

| Paso | Acción | Resultado Esperado |
|------|--------|-------------------|
| 1 | Cargar guardar-test.docx | Contenido visible |
| 2 | Realizar reemplazo de texto | Texto cambia a "...texto modificado." |
| 3 | Clic en "Guardar Como" | Se abre diálogo de selección de carpeta |
| 4 | Navegar a C:\test-results\ | Carpeta se muestra en el diálogo |
| 5 | Clic en "Seleccionar carpeta" | Diálogo se cierra |
| 6 | Verificar mensaje | Aparece: "Archivos guardados en C:\test-results\" |
| 7 | Clic en "Aceptar" | Mensaje se cierra |
| 8 | Abrir Windows Explorer | - |
| 9 | Navegar a C:\test-results\ | - |
| 10 | Verificar archivo guardado | Existe "guardar-test.docx" en la carpeta |
| 11 | Verificar tamaño del archivo | Tamaño similar al original (±5%) |
| 12 | Abrir archivo con Microsoft Word | Archivo se abre sin errores |
| 13 | Verificar contenido | Texto muestra "...texto modificado." |
| 14 | Cerrar Microsoft Word | - |
| 15 | Volver a la aplicación | Aplicación sigue abierta con el documento |


## Resultado Esperado

Los archivos se guardan correctamente en la carpeta seleccionada, los cambios persisten en los archivos guardados, y los archivos pueden abrirse en Microsoft Word sin problemas.

## Postcondiciones
- Los archivos están guardados en la carpeta destino
- Los archivos originales pueden estar o no modificados (según carpeta elegida)
- La aplicación sigue funcionando normalmente
- Los archivos guardados son compatibles con Microsoft Word

## Dependencias
- **Prerrequisito**: TC-001 (Carga), TC-004 o TC-005 (Modificación)

## Notas Adicionales
- **Tiempo estimado**: 4 minutos
- **Recomendación**: Guardar en carpeta diferente para no sobrescribir originales
- **Prueba adicional**: Guardar múltiples archivos modificados

## Evidencias Requeridas
- [ ] Screenshot del diálogo de selección de carpeta
- [ ] Screenshot del mensaje "Archivos guardados en..."
- [ ] Screenshot del archivo en Windows Explorer
- [ ] Screenshot del archivo abierto en Microsoft Word

## Criterios de Fallo
Falla si:
- No se guarda el archivo
- Se guarda en ubicación incorrecta
- Los cambios no persisten en el archivo guardado
- El archivo guardado está corrupto
- No se puede abrir en Microsoft Word
- No muestra mensaje de confirmación

## Historial de Ejecuciones

| Fecha | Ejecutado por | Build | Resultado | Defectos | Observaciones |
|-------|---------------|-------|-----------|----------|---------------|
| 22/10/2025 | Rosa QA | v1.0 | PASS | Ninguno | Funciona correctamente |

# TC-009: Verificar Función Limpiar Interfaz

## Objetivo
Verificar que la función "Limpiar" borra el contenido visible del área de texto y los campos de búsqueda/reemplazo sin afectar los archivos cargados en memoria.

## Precondiciones
- [ ] La aplicación está abierta
- [ ] Hay un archivo Word cargado
- [ ] Hay texto en el campo "Buscar..."
- [ ] Hay resaltados en el área de texto

## Datos de Prueba

**Archivo cargado**: limpiar-test.docx
**Campo Buscar**: "test"
**Campo Reemplazar**: "prueba"
**Resaltados**: Múltiples coincidencias en amarillo

## Pasos de Ejecución

| Paso | Acción | Resultado Esperado |
|------|--------|-------------------|
| 1 | Cargar limpiar-test.docx | Contenido visible en área de texto |
| 2 | Escribir "test" en "Buscar..." | Coincidencias resaltadas en amarillo |
| 3 | Escribir "prueba" en "Reemplazar por..." | Texto visible en el campo |
| 4 | Verificar estado antes de limpiar | Área de texto con contenido, campos llenos, resaltados visibles |
| 5 | Clic en botón "Limpiar" | - |
| 6 | Verificar área de texto | Completamente vacía (sin texto) |
| 7 | Verificar campo "Buscar..." | Vacío (sin texto) |
| 8 | Verificar campo "Reemplazar por..." | Vacío (sin texto) |
| 9 | Verificar resaltados | No hay resaltados visibles |
| 10 | Clic en "Siguiente >>" (si hay múltiples docs) | El contenido del siguiente documento aparece |
| 11 | Clic en "<< Anterior" | El contenido del primer documento reaparece |
| 12 | Verificar contenido | Todo el texto está intacto (no se perdió) |


## Resultado Esperado

La función "Limpiar" borra la visualización (área de texto y campos) pero NO elimina los archivos de la memoria, permitiendo recuperar el contenido mediante navegación.


## Postcondiciones
- La interfaz está limpia visualmente
- Los archivos permanecen en memoria (self.docs)
- Se puede recuperar el contenido navegando
- Los archivos NO se modifican

## Dependencias
- **Prerrequisito**: TC-001 (Carga)


## Notas Adicionales
- **Tiempo estimado**: 2 minutos
- **Característica**: Es una limpieza visual, no funcional


## Evidencias Requeridas
- [ ] Screenshot ANTES de limpiar (con contenido)
- [ ] Screenshot DESPUÉS de limpiar (todo vacío)
- [ ] Screenshot mostrando recuperación del contenido


## Criterios de Fallo
Falla si:
- No limpia el área de texto
- No limpia los campos de entrada
- No elimina los resaltados
- Elimina los archivos de memoria (no se puede recuperar contenido)
- Genera error


## Historial de Ejecuciones

| Fecha | Ejecutado por | Build | Resultado | Defectos | Observaciones |
|-------|---------------|-------|-----------|----------|---------------|
| 22/10/2025 | Rosa QA | v1.0 | PASS | Ninguno | Funciona correctamente |


# TC-010: Verificar Manejo de Errores - Archivo No Válido


## Objetivo
Verificar que la aplicación maneja correctamente los intentos de cargar archivos no válidos y muestra mensajes de error apropiados sin causar crash.


## Precondiciones
- [ ] La aplicación está abierta
- [ ] Existen archivos de prueba con formatos no soportados

## Datos de Prueba

Archivos de prueba a intentar cargar:

| Archivo | Tipo | Extensión | Resultado Esperado |
|---------|------|-----------|-------------------|
| documento.doc | Word antiguo | .doc | Error o no se muestra en diálogo |
| documento.pdf | PDF | .pdf | Error o no se muestra en diálogo |
| documento.txt | Texto plano | .txt | Error o no se muestra en diálogo |
| corrupto.docx | Word corrupto | .docx | Mensaje de error al cargar |
| vacio.docx | Word vacío | .docx | Carga pero área de texto vacía |

## Pasos de Ejecución

### Escenario 1: Intentar cargar archivo .doc (Word antiguo)

| Paso | Acción | Resultado Esperado |
|------|--------|-------------------|
| 1 | Clic en "Cargar Word" | Diálogo de selección se abre |
| 2 | Navegar a carpeta de prueba | - |
| 3 | Observar archivos mostrados | Solo archivos .docx son visibles (filtro activo) |
| 4 | Cambiar filtro a "Todos los archivos" | Archivo .doc ahora visible |
| 5 | Seleccionar documento.doc | Archivo seleccionado |
| 6 | Clic en "Abrir" | Aparece mensaje de error o no carga |
| 7 | Verificar mensaje | Mensaje claro indicando formato no soportado |
| 8 | Verificar aplicación | No se cierra, sigue funcionando |

### Escenario 2: Intentar cargar archivo corrupto

| Paso | Acción | Resultado Esperado |
|------|--------|-------------------|
| 1 | Clic en "Cargar Word" | Diálogo se abre |
| 2 | Seleccionar corrupto.docx | Archivo seleccionado |
| 3 | Clic en "Abrir" | Aparece mensaje de error |
| 4 | Verificar mensaje | Indica que el archivo está corrupto o no se puede leer |
| 5 | Clic en "Aceptar" | Mensaje se cierra |
| 6 | Verificar aplicación | Sigue funcionando sin crash |

### Escenario 3: Cargar archivo Word vacío

| Paso | Acción | Resultado Esperado |
|------|--------|-------------------|
| 1 | Clic en "Cargar Word" | Diálogo se abre |
| 2 | Seleccionar vacio.docx | Archivo seleccionado |
| 3 | Clic en "Abrir" | El archivo se carga sin error |
| 4 | Verificar área de texto | Área de texto vacía o muestra espacios en blanco |
| 5 | Verificar etiqueta | Muestra "Archivo 1/1: vacio.docx" |

## Resultado Esperado

La aplicación maneja correctamente archivos no válidos, muestra mensajes de error apropiados y NO se cierra inesperadamente.

## Postcondiciones
- La aplicación permanece estable y funcional
- No se carga contenido inválido
- El usuario es informado del problema
- Puede intentar cargar otro archivo

## Dependencias
- **Casos relacionados**: TC-001 (Carga válida)

## Notas Adicionales
- **Tiempo estimado**: 6 minutos (3 escenarios)
- **Objetivo secundario**: Verificar robustez de la aplicación

## Evidencias Requeridas
- [ ] Screenshot del diálogo con filtro .docx
- [ ] Screenshot del mensaje de error para archivo .doc
- [ ] Screenshot del mensaje de error para archivo corrupto
- [ ] Screenshot de archivo vacío cargado

## Criterios de Fallo
Falla si:
- La aplicación se cierra (crash)
- Carga archivos no .docx sin error
- No muestra mensaje de error
- El mensaje de error es confuso o técnico
- Carga archivo corrupto y muestra contenido basura
- Permite operaciones sobre archivo no cargado

## Historial de Ejecuciones

| Fecha | Ejecutado por | Build | Resultado | Defectos | Observaciones |
|-------|---------------|-------|-----------|----------|---------------|
| 22/10/2025 | Rosa QA | v1.0 | PASS | Ninguno | Manejo de errores adecuado |

# Resumen de Casos de Prueba

## Estadísticas

| Métrica | Valor |
|---------|-------|
| **Total de Casos** | 10 |
| **Prioridad Alta** | 6 (TC-001 a TC-005, TC-008) |
| **Prioridad Media** | 3 (TC-006, TC-007, TC-010) |
| **Prioridad Baja** | 1 (TC-009) |
| **Tipo Positivo** | 9 |
| **Tipo Negativo** | 1 (TC-010) |
| **Estado Activo** | 10 |

## Cobertura de Módulos

| Módulo | Casos de Prueba | Cobertura |
|--------|----------------|-----------|
| Gestión de Archivos | TC-001, TC-002 | 100% |
| Búsqueda | TC-003 | 100% |
| Reemplazo | TC-004, TC-005 | 100% |
| Navegación | TC-006 | 100% |
| Historial | TC-007 | 100% |
| Guardado | TC-008 | 100% |
| UI | TC-009 | 100% |
| Validación | TC-010 | 100% |

## Matriz de Trazabilidad

| Requisito | Casos de Prueba | Estado |
|-----------|----------------|--------|
| REQ-001: Carga archivos | TC-001, TC-002, TC-010 | Cubierto |
| REQ-002: Búsqueda texto | TC-003 | Cubierto |
| REQ-003: Reemplazo selectivo | TC-004 | Cubierto |
| REQ-004: Reemplazo masivo | TC-005 | Cubierto |
| REQ-005: Navegación | TC-006 | Cubierto |
| REQ-006: Deshacer | TC-007 | Cubierto |
| REQ-007: Guardado | TC-008 | Cubierto |
| REQ-008: Limpiar UI | TC-009 | Cubierto |

## Dependencias entre Casos

```
TC-001 (Carga Individual)
  ├─> TC-003 (Búsqueda)
  │     └─> TC-004 (Reemplazo Selectivo)
  │           └─> TC-007 (Deshacer)
  ├─> TC-005 (Reemplazo Masivo)
  ├─> TC-008 (Guardado)
  └─> TC-009 (Limpiar)

TC-002 (Carga Múltiple)
  ├─> TC-005 (Reemplazo Masivo)
  └─> TC-006 (Navegación)

TC-010 (Manejo Errores) - Independiente
```

## Tiempo Estimado Total de Ejecución

| Ciclo | Tiempo |
|-------|--------|
| **Ejecución completa** | 40 minutos |
| **Casos prioritarios (Alta)** | 28 minutos |
| **Pruebas de humo** | 15 minutos (TC-001, TC-003, TC-005, TC-008) |

