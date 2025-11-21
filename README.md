
### Instalación

1. **Descarga el ejecutable**
   - Descarga `EditorWordMasivo.exe` [![Latest Release](https://img.shields.io/github/v/release/rosafg/word-editor?label=Descargar%20%C3%BAltima%20versi%C3%B3n)](https://github.com/rosafg/word-editor/releases/latest)
   
2. **Ejecuta la aplicación**
   - Doble clic en el archivo `.exe`
   - Si Windows SmartScreen muestra advertencia:
   - Haz clic en **"Más información"**
   - Luego en **"Ejecutar de todas formas"**

3. **¡Listo!** La aplicación se abrirá automáticamente

**Requisitos:**
- Windows 10 o superior
- No requiere instalación de Python
- No requiere permisos de administrador

---

##  Interfaz de la Aplicación

```
┌─────────────────────────────────────────────────────┐
│  [Cargar Word]  [Cargar Varios Word]                │
├─────────────────────────────────────────────────────┤
│  Buscar...                                          │
│  Reemplazar por...                                  │
├─────────────────────────────────────────────────────┤
│  [Reemplazar] [Reemplazar Todo] [Deshacer]          │
│  [Limpiar] [Guardar Como]                           │
├─────────────────────────────────────────────────────┤
│  [<< Anterior] [Siguiente >>]  Archivo 1/3: doc.docx│
├─────────────────────────────────────────────────────┤
│                                                     │
│              Área de Texto                          │
│         (Contenido del documento)                   │
│                                                     │
└─────────────────────────────────────────────────────┘
```
![Demo 1](assets/screenshots/Editor_Word_Masivo.gif)
Carga de varios word

![Demo 2](assets/screenshots/Editor_Word_Unitario.gif)
Carga de 1 word

---

##  Funciones Principales

###  Cargar Documentos

#### **Opción A: Cargar un Solo Archivo**

1. Haz clic en el botón **"Cargar Word"**
2. Se abrirá el explorador de archivos
3. Selecciona un archivo `.docx`
4. Haz clic en **"Abrir"**
5. El contenido aparecerá en el área de texto

**Resultado esperado:**
- El documento se muestra completo
- Aparece el nombre del archivo: "Archivo 1/1: nombre.docx"

---

#### **Opción B: Cargar Múltiples Archivos**

1. Haz clic en el botón **"Cargar Varios Word"**
2. Se abrirá el explorador de archivos
3. Selecciona varios archivos:
   - Mantén presionada la tecla **Ctrl**
   - Haz clic en cada archivo que desees seleccionar
4. Haz clic en **"Abrir"**
5. Se cargará el primer documento

**Resultado esperado:**
- Se muestra el primer documento
- Aparece "Archivo 1/X: nombre.docx" (donde X = total de archivos)
- Puedes navegar entre documentos con los botones de navegación

---

###  Buscar Texto

1. Escribe el texto a buscar en el campo **"Buscar..."**
2. Las coincidencias se resaltarán automáticamente en **amarillo**
3. El resaltado se actualiza mientras escribes

**Características:**
- Búsqueda en tiempo real
- **No** distingue entre mayúsculas y minúsculas
- Busca palabras completas o fragmentos
- Funciona en el documento actual

**Ejemplo:**
```
Buscar: "cliente"
Resultado: Resalta "cliente", "Cliente", "CLIENTE"
```

---

###  Reemplazar Texto

#### **Opción A: Reemplazo Selectivo** (Solo documento actual)

**Uso ideal:** Cuando quieres revisar cada coincidencia antes de reemplazarla

1. Escribe el texto a buscar en **"Buscar..."**
2. Escribe el texto nuevo en **"Reemplazar por..."**
3. Haz clic en **"Reemplazar"**
4. Para cada coincidencia encontrada:
   -  Aparecerá un diálogo preguntando:
     ```
     ¿Reemplazar 'texto_original' en el párrafo X?
     [Sí] [No]
     ```
5. Haz clic en **Sí** para reemplazar o **No** para omitir
6.  Al finalizar, verás un mensaje: "Reemplazo selectivo completado"

**Ejemplo práctico:**
```
Documento original:
"El cliente Juan visitó la tienda. El cliente está satisfecho."

Buscar: "cliente"
Reemplazar por: "comprador"

Proceso:
- ¿Reemplazar 'cliente' en párrafo 1? → SÍ
  → "El comprador Juan visitó la tienda..."
  
- ¿Reemplazar 'cliente' en párrafo 1? → NO
  → "...El cliente está satisfecho." (sin cambios)
```

---

#### **Opción B: Reemplazo Masivo** (Todos los documentos)

**Uso ideal:** Cuando estás seguro del cambio y quieres aplicarlo a todo

1. Escribe el texto a buscar en **"Buscar..."**
2. Escribe el texto nuevo en **"Reemplazar por..."**
3. Haz clic en **"Reemplazar Todo"**
4. Verás un mensaje: "Se reemplazaron X coincidencias en todos los documentos"

**IMPORTANTE:**
- Este cambio afecta **TODOS** los documentos cargados
- No pide confirmación para cada coincidencia
- Puedes deshacerlo con el botón "Deshacer"

**Ejemplo práctico:**
```
3 documentos cargados con el texto:
Doc1: "correo@viejo.com"
Doc2: "Contacto: correo@viejo.com"
Doc3: "Enviar a correo@viejo.com"

Buscar: "correo@viejo.com"
Reemplazar por: "correo@nuevo.com"

Resultado: Todas las instancias se reemplazan en los 3 archivos
→ "Se reemplazaron 3 coincidencias en todos los documentos"
```

---

###  Navegar Entre Documentos

**Solo disponible cuando cargas múltiples archivos**

**Botones de navegación:**
- **"<< Anterior"**: Ve al documento anterior
- **"Siguiente >>"**: Ve al documento siguiente

**Indicador de posición:**
- Muestra: "Archivo 2/5: informe-ventas.docx"
- Indica: documento actual / total de documentos

**Atajos:**
- Si estás en el primer documento, "Anterior" no hace nada
- Si estás en el último documento, "Siguiente" no hace nada

---

###  Deshacer Cambios

**¿Cuándo usar?**
- Después de un reemplazo incorrecto
- Si te arrepientes de un cambio
- Para volver al estado anterior

**Cómo usar:**
1. Haz clic en **"Deshacer"**
2. Se revierte la última operación de reemplazo
3. Puedes deshacer múltiples veces

**Limitaciones:**
- Solo funciona durante la sesión actual
- Si cierras la app, se pierde el historial
- Una vez que guardas, no puedes deshacer

---

###  Guardar Archivos

**IMPORTANTE:** Los cambios NO son permanentes hasta que guardes

**Proceso:**
1. Haz clic en **"Guardar Como"**
2. Se abre el explorador de carpetas
3. Selecciona la carpeta de destino
4. Haz clic en **"Seleccionar carpeta"**
5. Todos los archivos modificados se guardan en esa carpeta

**Notas:**
- Los archivos mantienen su nombre original
- Se sobrescribirán si ya existen en la carpeta
- Todos los documentos cargados se guardan (modificados o no)

**Recomendación:** Guarda en una carpeta diferente a la original para no perder los archivos originales

---

###  Limpiar Interfaz

**¿Qué limpia este botón?**
- Borra el área de texto
- Limpia el campo "Buscar..."
- Limpia el campo "Reemplazar por..."
- Quita todos los resaltados amarillos

**IMPORTANTE:**
- No cierra los archivos cargados
- No elimina el historial de deshacer
- Solo limpia la visualización
- Para ver el contenido de nuevo, cambia de documento o usa navegación

---

##  Casos de Uso Prácticos

### **Caso 1: Corregir Error Ortográfico en 10 Documentos**

**Situación:** Escribiste mal "recivir" en lugar de "recibir" en múltiples informes

**Pasos:**
1. Clic en **"Cargar Varios Word"**
2. Selecciona los 10 documentos (Ctrl + clic)
3. En **"Buscar..."** escribe: `recivir`
4. En **"Reemplazar por..."** escribe: `recibir`
5. Clic en **"Reemplazar Todo"**
6. Mensaje: "Se reemplazaron 15 coincidencias en todos los documentos"
7. Clic en **"Guardar Como"**
8. Selecciona carpeta de destino
9. ¡Corrección masiva completada!

---

### **Caso 2: Actualizar Información de Contacto**

**Situación:** Cambió el teléfono de contacto de la empresa

**Pasos:**
1. Carga los documentos con información de contacto
2. En **"Buscar..."** escribe: `555-1234`
3. En **"Reemplazar por..."** escribe: `555-9999`
4. Clic en **"Reemplazar"** (selectivo)
5. Revisa cada coincidencia antes de confirmar
6. Si te equivocas, usa **"Deshacer"**
7. Guarda los cambios

---

### **Caso 3: Verificar Menciones de un Término**

**Situación:** Quieres ver todas las veces que mencionas "presupuesto"

**Pasos:**
1. Carga el documento
2. En **"Buscar..."** escribe: `presupuesto`
3. Todas las menciones se resaltan en amarillo
4. Navega por el documento para revisarlas
5. **No hagas reemplazo**, solo revisa
6. Usa **"Limpiar"** cuando termines

---

### **Caso 4: Reemplazar Solo en Algunos Documentos**

**Situación:** Tienes 5 documentos, pero solo quieres cambiar texto en 2

**Pasos:**
1. Carga solo los 2 documentos que quieres modificar
2. Realiza los reemplazos
3. Guarda
4. Luego carga los otros 3 documentos si necesitas revisarlos

---

##  Advertencias Importantes

###  Limitaciones de la Aplicación

1. **Solo trabaja con texto plano**
   -  No preserva: negrita, cursiva, colores, subrayado
   -  No preserva: tablas, imágenes, gráficos
   -  Solo preserva: el texto y los saltos de línea

2. **Formato del archivo**
   -  Solo acepta archivos `.docx` (Word moderno)
   -  No acepta: `.doc` (Word antiguo), `.pdf`, `.txt`

3. **Historial de cambios**
   -  Puedes deshacer durante la sesión
   -  Si cierras la app, pierdes el historial
   -  Una vez guardado, no puedes deshacer

###  Buenas Prácticas

1. **Siempre haz respaldo**
   - Guarda una copia de los archivos originales antes de editar

2. **Prueba primero con "Reemplazar"**
   - Usa reemplazo selectivo antes del masivo
   - Verifica que los cambios sean correctos

3. **Revisa antes de guardar**
   - Navega por los documentos modificados
   - Verifica que todo quedó como esperabas

4. **Guarda en carpeta diferente**
   - No sobrescribas los archivos originales
   - Facilita comparar versiones

5. **Usa búsquedas específicas**
   - Busca frases completas cuando sea posible
   - Evita términos muy genéricos que puedan dar muchas coincidencias

---

## Solución de Problemas

### Problema: "Windows bloqueó el ejecutable"
**Solución:**
1. Clic derecho en el archivo → Propiedades
2. Marca "Desbloquear" → Aplicar
3. O usa: Más información → Ejecutar de todas formas

### Problema: "No puedo seleccionar múltiples archivos"
**Solución:**
- Mantén presionada la tecla **Ctrl** mientras haces clic en cada archivo

### Problema: "El contenido no se muestra correctamente"
**Solución:**
- Verifica que el archivo sea `.docx` (no `.doc`)
- Intenta abrir el archivo en Word primero para verificar que no esté corrupto

### Problema: "Los cambios no se guardaron"
**Solución:**
- Verifica que hayas hecho clic en "Guardar Como"
- Asegúrate de tener permisos de escritura en la carpeta destino

### Problema: "Reemplacé texto equivocado"
**Solución:**
- Haz clic en **"Deshacer"** inmediatamente
- Si ya cerraste la app, usa tus respaldos originales

---

##  Soporte

Si encuentras algún problema o tienes sugerencias:
- Email: [rosafuegos@gmail.com]
- Reporta bugs en: [GitHub Issues]
---

##  Resumen de Controles

| Botón | Función |
|-------|---------|
| **Cargar Word** | Abre un solo archivo .docx |
| **Cargar Varios Word** | Abre múltiples archivos .docx |
| **Buscar...** | Campo para texto a buscar (resalta automáticamente) |
| **Reemplazar por...** | Campo para texto de reemplazo |
| **Reemplazar** | Reemplazo selectivo (pregunta uno por uno) |
| **Reemplazar Todo** | Reemplazo masivo en todos los documentos |
| **Deshacer** | Revierte el último cambio |
| **Limpiar** | Limpia campos y área de texto |
| **Guardar Como** | Guarda todos los archivos modificados |
| **<< Anterior** | Documento anterior (si hay varios) |
| **Siguiente >>** | Documento siguiente (si hay varios) |
