# Arquitectura de la Aplicación - Editor Word Masivo

## Información del Documento

| Campo | Detalle |
|-------|---------|
| **Proyecto** | Editor Word Masivo v1.0 |
| **Documento** | Arquitectura de la Aplicación |
| **Versión** | 1.0 |
| **Fecha** | 22/10/2025 |
| **Autor** | Rosita QA |

---

## 1. Introducción

### 1.1 Propósito del Documento
Este documento describe la arquitectura técnica de la aplicación Editor Word Masivo, incluyendo su estructura de componentes, tecnologías utilizadas, flujos de datos y diseño interno. El objetivo es proporcionar una comprensión clara de cómo funciona la aplicación desde una perspectiva técnica.

### 1.2 Audiencia
- Testers QA que necesitan entender el funcionamiento interno
- Desarrolladores que realizarán mantenimiento o mejoras
- Stakeholders técnicos interesados en la arquitectura

### 1.3 Alcance
Este documento cubre:
- Arquitectura de alto nivel
- Componentes principales y sus responsabilidades
- Tecnologías y dependencias
- Flujos de datos
- Estructura de archivos
- Patrones de diseño utilizados

---

## 2. Visión General de la Arquitectura

### 2.1 Tipo de Aplicación
**Aplicación de escritorio standalone** desarrollada en Python con interfaz gráfica basada en CustomTkinter.

**Características principales:**
- Aplicación monolítica (todo en un solo proceso)
- Sin conectividad de red
- Sin base de datos externa
- Almacenamiento en memoria durante la sesión
- Procesamiento local de archivos

### 2.2 Arquitectura de Alto Nivel

```
┌─────────────────────────────────────────────────────────┐
│                    CAPA DE PRESENTACIÓN                 │
│  (CustomTkinter - Interfaz Gráfica de Usuario)         │
│                                                          │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐ │
│  │   Botones    │  │   Entries    │  │   TextArea   │ │
│  └──────────────┘  └──────────────┘  └──────────────┘ │
└─────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────┐
│                     CAPA DE LÓGICA                      │
│  (Clase WordEditorMassive - Controlador Principal)     │
│                                                          │
│  ┌──────────────────────────────────────────────────┐  │
│  │  Métodos de Negocio:                             │  │
│  │  - load_word()                                   │  │
│  │  - search_and_highlight()                        │  │
│  │  - replace_text_selective()                      │  │
│  │  - replace_all_docs()                            │  │
│  │  - undo()                                        │  │
│  │  - save_file()                                   │  │
│  └──────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────┐
│                    CAPA DE DATOS                        │
│  (Variables de Instancia - Almacenamiento en Memoria)  │
│                                                          │
│  - self.docs: List[Document]      (objetos Word)       │
│  - self.file_paths: List[str]     (rutas archivos)     │
│  - self.current_index: int        (doc actual)         │
│  - self.history: List             (historial)          │
└─────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────┐
│                 CAPA DE PERSISTENCIA                    │
│  (Sistema de Archivos - Lectura/Escritura)             │
│                                                          │
│  ┌──────────────┐          ┌──────────────┐           │
│  │ python-docx  │          │   OS / IO    │           │
│  │  Document    │          │  FileDialog  │           │
│  └──────────────┘          └──────────────┘           │
└─────────────────────────────────────────────────────────┘
```

---

## 3. Componentes Principales

### 3.1 Clase Principal: WordEditorMassive

**Responsabilidad:** Controlador principal que maneja toda la lógica de la aplicación.

**Herencia:** 
```python
class WordEditorMassive(ctk.CTk)
```
Hereda de `customtkinter.CTk` (ventana principal de CustomTkinter)

**Atributos de Instancia:**

| Atributo | Tipo | Propósito |
|----------|------|-----------|
| `self.docs` | `List[Document]` | Lista de objetos Document (python-docx) cargados |
| `self.file_paths` | `List[str]` | Rutas completas de los archivos cargados |
| `self.current_index` | `int` | Índice del documento actual siendo visualizado |
| `self.history` | `List[List[Document]]` | Historial de estados para función deshacer |

**Métodos Principales:**

```python
__init__(self)                    # Constructor, inicializa la UI
load_word(self)                   # Carga un solo archivo Word
load_many_words(self)             # Carga múltiples archivos Word
update_text_area(self)            # Actualiza visualización del documento
update_file_label(self)           # Actualiza etiqueta de archivo actual
highlight_matches(self)           # Resalta coincidencias de búsqueda
replace_text_selective(self)      # Reemplazo selectivo (uno por uno)
replace_all_docs(self)            # Reemplazo masivo (todos)
undo(self)                        # Deshace último cambio
clear_text(self)                  # Limpia interfaz
save_file(self)                   # Guarda archivos modificados
prev_doc(self)                    # Navega a documento anterior
next_doc(self)                    # Navega a documento siguiente
```

---

### 3.2 Componentes de Interfaz Gráfica (UI)

#### 3.2.1 Frames (Contenedores)

**top_frame:**
- Contiene botones de carga de archivos
- Alineación horizontal
- Posición: Parte superior de la ventana

**btn_frame:**
- Contiene botones de acción (Reemplazar, Deshacer, Guardar, etc.)
- Alineación horizontal
- Posición: Centro de la ventana

**nav_frame:**
- Contiene botones de navegación y etiqueta de archivo
- Alineación horizontal
- Posición: Debajo de btn_frame

#### 3.2.2 Widgets Principales

**Botones (CTkButton):**
```python
self.load_btn           # "Cargar Word"
self.load_many_btn      # "Cargar Varios Word"
self.replace_btn        # "Reemplazar"
self.replace_all_btn    # "Reemplazar Todo"
self.undo_btn           # "Deshacer"
self.clear_btn          # "Limpiar"
self.save_btn           # "Guardar Como"
self.prev_btn           # "<< Anterior"
self.next_btn           # "Siguiente >>"
```

**Campos de Entrada (CTkEntry):**
```python
self.search_entry       # Campo de búsqueda
self.replace_entry      # Campo de reemplazo
```

**Área de Texto (CTkTextbox):**
```python
self.text_area          # Visualización del contenido del documento
```

**Etiquetas (CTkLabel):**
```python
self.file_label         # Muestra "Archivo X/Y: nombre.docx"
```

---

## 4. Flujos de Datos

### 4.1 Flujo de Carga de Archivo

```
┌──────────────┐
│   Usuario    │
│ Click botón  │
└──────┬───────┘
       │
       ▼
┌──────────────────────────┐
│ filedialog.askopenfile() │
│  (diálogo del sistema)   │
└──────────┬───────────────┘
           │
           ▼ (ruta del archivo)
┌──────────────────────────┐
│   Document(path)         │
│   (python-docx)          │
└──────────┬───────────────┘
           │
           ▼ (objeto Document)
┌──────────────────────────┐
│  self.docs.append(doc)   │
│  self.file_paths.append  │
└──────────┬───────────────┘
           │
           ▼
┌──────────────────────────┐
│  update_text_area()      │
│  (mostrar en UI)         │
└──────────────────────────┘
```

### 4.2 Flujo de Búsqueda y Resaltado

```
┌──────────────┐
│   Usuario    │
│ Escribe en   │
│ search_entry │
└──────┬───────┘
       │
       ▼ (evento KeyRelease)
┌──────────────────────────┐
│  highlight_matches()     │
└──────────┬───────────────┘
           │
           ▼
┌──────────────────────────┐
│  re.compile(pattern)     │
│  (crear expresión regex) │
└──────────┬───────────────┘
           │
           ▼
┌──────────────────────────┐
│  pattern.search()        │
│  (buscar coincidencias)  │
└──────────┬───────────────┘
           │
           ▼
┌──────────────────────────┐
│  text_area.tag_add()     │
│  (resaltar en amarillo)  │
└──────────────────────────┘
```

### 4.3 Flujo de Reemplazo Selectivo

```
┌──────────────┐
│   Usuario    │
│ Click        │
│ "Reemplazar" │
└──────┬───────┘
       │
       ▼
┌──────────────────────────┐
│ Validar campos           │
│ (buscar no vacío)        │
└──────────┬───────────────┘
           │
           ▼
┌──────────────────────────┐
│ Guardar en historial     │
│ self.history.append()    │
└──────────┬───────────────┘
           │
           ▼
┌──────────────────────────┐
│ Buscar coincidencias     │
│ pattern.finditer()       │
└──────────┬───────────────┘
           │
           ▼ (lista matches)
┌──────────────────────────┐
│ Para cada coincidencia:  │
│ messagebox.askyesno()    │
└──────────┬───────────────┘
           │
           ▼ (respuesta usuario)
┌──────────────────────────┐
│ Si SÍ: reemplazar texto  │
│ para.text = nuevo_texto  │
└──────────┬───────────────┘
           │
           ▼
┌──────────────────────────┐
│  update_text_area()      │
│  (actualizar UI)         │
└──────────────────────────┘
```

### 4.4 Flujo de Guardado

```
┌──────────────┐
│   Usuario    │
│ Click        │
│ "Guardar"    │
└──────┬───────┘
       │
       ▼
┌──────────────────────────┐
│ filedialog.askdirectory()│
│ (seleccionar carpeta)    │
└──────────┬───────────────┘
           │
           ▼ (ruta carpeta)
┌──────────────────────────┐
│ Para cada documento:     │
│ en self.docs[]           │
└──────────┬───────────────┘
           │
           ▼
┌──────────────────────────┐
│ doc.save(ruta_completa)  │
│ (python-docx)            │
└──────────┬───────────────┘
           │
           ▼
┌──────────────────────────┐
│ messagebox.showinfo()    │
│ (confirmar guardado)     │
└──────────────────────────┘
```

---

## 5. Gestión de Estado

### 5.1 Estado de la Aplicación

**Variables de Estado Principal:**

```python
self.docs = []              # Lista de documentos cargados
self.file_paths = []        # Rutas de archivos
self.current_index = 0      # Documento actual
self.history = []           # Historial de cambios
```

**Transiciones de Estado:**

| Acción del Usuario | Cambio de Estado |
|-------------------|------------------|
| Cargar archivo | `self.docs` se llena, `current_index = 0` |
| Navegar siguiente | `current_index += 1` |
| Navegar anterior | `current_index -= 1` |
| Reemplazar texto | `self.docs` modificado, `history` actualizado |
| Deshacer | Restaurar desde `history`, `docs` revertido |
| Limpiar | UI limpia, pero `docs` intacto |
| Cerrar app | Todo el estado se pierde |

### 5.2 Gestión del Historial

**Implementación:**
```python
self.history = [copy.deepcopy(self.docs)]  # Estado inicial
```

**Cuando se realiza un cambio:**
```python
self.history.append(copy.deepcopy(self.docs))  # Guardar estado
```

**Cuando se deshace:**
```python
self.history.pop()                          # Eliminar último
self.docs = copy.deepcopy(self.history[-1]) # Restaurar anterior
```

**Características:**
- Historial ilimitado durante la sesión
- Usa `copy.deepcopy()` para clonar objetos completos
- Se pierde al cerrar la aplicación
- No hay persistencia en disco

---

## 6. Tecnologías y Dependencias

### 6.1 Lenguaje Base

**Python 3.13**
- Lenguaje interpretado
- Multiplataforma (aunque el .exe es solo Windows)
- Tipado dinámico

### 6.2 Librerías Principales

#### 6.2.1 CustomTkinter (ctk)

**Versión:** 5.2.0 (aproximada)

**Propósito:** Framework de interfaz gráfica moderna basado en Tkinter

**Componentes Utilizados:**
- `CTk` - Ventana principal
- `CTkFrame` - Contenedores
- `CTkButton` - Botones
- `CTkEntry` - Campos de texto
- `CTkTextbox` - Área de texto multilinea
- `CTkLabel` - Etiquetas

**Ventajas:**
- Apariencia moderna (vs Tkinter tradicional)
- Temas oscuro/claro
- Widgets estilizados
- Compatible con Tkinter estándar

#### 6.2.2 python-docx

**Versión:** 1.1.0 (aproximada)

**Propósito:** Lectura y escritura de archivos Word (.docx)

**Uso en la aplicación:**
```python
from docx import Document

# Cargar archivo
doc = Document(path)

# Leer párrafos
for para in doc.paragraphs:
    texto = para.text

# Modificar texto
para.text = nuevo_texto

# Guardar
doc.save(ruta)
```

**Limitaciones:**
- Solo soporta .docx (no .doc antiguo)
- Al modificar `para.text`, se pierde el formato original
- No maneja tablas, imágenes, encabezados

#### 6.2.3 tkinter (estándar)

**Propósito:** Funcionalidades adicionales de Tkinter estándar

**Módulos utilizados:**
```python
from tkinter import filedialog   # Diálogos de archivo
from tkinter import messagebox   # Mensajes al usuario
from tkinter import PhotoImage   # Carga de icono (no funcional)
```

#### 6.2.4 re (Regular Expressions)

**Propósito:** Búsqueda de patrones de texto

**Uso:**
```python
import re

pattern = re.compile(re.escape(search_text), re.IGNORECASE)
matches = pattern.finditer(text)
new_text = pattern.sub(replace_text, original_text)
```

**Características:**
- `re.escape()` - Escapa caracteres especiales
- `re.IGNORECASE` - Búsqueda sin distinción de mayúsculas
- `finditer()` - Encuentra todas las coincidencias
- `sub()` - Reemplaza coincidencias

#### 6.2.5 os

**Propósito:** Operaciones del sistema operativo

**Uso:**
```python
import os

os.path.basename(ruta)        # Extraer nombre de archivo
os.path.join(carpeta, archivo) # Construir ruta
os.path.exists(ruta)          # Verificar si existe
```

#### 6.2.6 copy

**Propósito:** Clonación profunda de objetos

**Uso:**
```python
import copy

copia = copy.deepcopy(self.docs)  # Clonar lista de Documents
```

**Necesario para:**
- Mantener historial de deshacer independiente
- Evitar referencias a objetos mutables

#### 6.2.7 fpdf (IMPORTADA PERO NO USADA)

**Estado:** Importada en línea 5 pero no implementada

```python
from fpdf import FPDF  # No se usa en la aplicación
```

**Funcionalidad planeada:** Exportación a PDF (no implementada)

---

### 6.3 Dependencias del Sistema

**Sistema Operativo:**
- Windows 10/11 (64-bit) - para ejecutable
- Python 3.8+ - para código fuente

**Requisitos adicionales:**
- No requiere Microsoft Word instalado (python-docx es independiente)
- No requiere conectividad de red
- No requiere permisos de administrador

---

## 7. Patrones de Diseño Utilizados

### 7.1 MVC Simplificado (Model-View-Controller)

Aunque no es MVC puro, la aplicación sigue una separación similar:

**Model (Modelo):**
- `self.docs` - Los datos (documentos Word)
- `self.file_paths` - Metadatos de archivos
- `self.history` - Estado histórico

**View (Vista):**
- Todos los widgets de CustomTkinter
- `self.text_area` - Visualización principal
- Etiquetas, botones, entries

**Controller (Controlador):**
- Métodos de la clase `WordEditorMassive`
- Maneja eventos de usuario
- Actualiza modelo y vista

### 7.2 Patrón Observer (Eventos)

CustomTkinter implementa el patrón Observer para eventos:

```python
self.search_entry.bind("<KeyRelease>", lambda e: self.highlight_matches())
self.replace_btn = CTkButton(text="...", command=self.replace_text_selective)
```

### 7.3 Memento (Historial de Deshacer)

Implementación básica del patrón Memento para deshacer:

```python
# Guardar estado (Memento)
self.history.append(copy.deepcopy(self.docs))

# Restaurar estado (Undo)
self.docs = copy.deepcopy(self.history[-1])
```

---

## 8. Estructura de Archivos

### 8.1 Estructura del Proyecto

```
word-editor-qa-portfolio/
│
├── src/
│   └── word_editor_massive.py    # Código principal (único archivo)
│
├── releases/
│   └── EditorWordMasivo.exe      # Ejecutable compilado
│
├── docs/
│   └── 03-documentacion-tecnica/
│       ├── arquitectura-app.md
│       ├── manual-instalacion.md
│       └── manual-usuario.md
│
├── test-cases/                    # Casos de prueba
├── test-results/                  # Resultados de testing
├── bug-reports/                   # Reportes de defectos
└── test-data/                     # Datos de prueba
```

### 8.2 Archivo Principal

**word_editor_massive.py:**
- Líneas de código: ~200
- Clases: 1 (WordEditorMassive)
- Funciones: 13 métodos
- Imports: 7 librerías

---

## 9. Limitaciones Técnicas

### 9.1 Limitaciones de Diseño

**Arquitectura Monolítica:**
- Todo en una sola clase
- Acoplamiento alto entre UI y lógica
- Dificulta unit testing
- No hay separación clara de responsabilidades

**Sin Capa de Abstracción:**
- Interacción directa con python-docx
- Sin interfaces o abstracciones
- Dificulta cambiar librería de Word

**Estado Global:**
- Variables de instancia compartidas
- No hay gestión de estado formal
- Historial global para todos los documentos

### 9.2 Limitaciones Funcionales

**Formato de Texto:**
- Solo maneja texto plano
- Pierde negrita, cursiva, colores
- No preserva tablas ni imágenes

**Historial:**
- No persistente (se pierde al cerrar)
- Consume memoria con documentos grandes
- No hay límite de niveles de deshacer

**Reemplazo Selectivo:**
- Bug conocido con múltiples coincidencias en mismo párrafo
- Los índices se invalidan después del primer reemplazo

**Navegación:**
- No hay indicación visual de documento modificado
- Historial no específico por documento

---

## 10. Consideraciones de Rendimiento

### 10.1 Uso de Memoria

**Almacenamiento en Memoria:**
```python
self.docs = [Document1, Document2, ...]  # Documentos completos en RAM
self.history = [Estado1, Estado2, ...]   # Clones profundos de documentos
```

**Impacto:**
- Cada documento carga completamente en RAM
- Historial duplica el uso de memoria
- Con 10 documentos de 1MB: ~20MB de RAM (aproximado)

### 10.2 Operaciones Costosas

**copy.deepcopy():**
- Operación pesada con documentos grandes
- Se ejecuta en cada reemplazo
- Puede causar lag con muchos documentos

**highlight_matches():**
- Se ejecuta en cada tecla presionada
- Con documentos grandes puede causar lag
- Usa regex que puede ser costoso

**Optimizaciones posibles:**
- Debouncing en búsqueda (esperar X ms)
- Límite de tamaño de historial
- Lazy loading de documentos

---

## 11. Seguridad

### 11.1 Consideraciones de Seguridad

**Sin Autenticación:**
- Cualquier usuario puede ejecutar la app
- No hay control de acceso

**Sin Validación de Archivos:**
- No verifica contenido malicioso
- Confía en que python-docx maneje archivos corruptos

**Sin Encriptación:**
- Archivos se guardan sin protección
- No hay cifrado de datos en memoria

**Sin Logs de Auditoría:**
- No registra quién hizo qué cambios
- No hay trazabilidad

### 11.2 Vectores de Ataque Potenciales

**Archivos Maliciosos:**
- .docx con macros (python-docx no ejecuta macros)
- Archivos corruptos que causan crash
- Path traversal en nombres de archivo

**Inyección:**
- No hay validación de entradas en búsqueda/reemplazo
- Regex complejos podrían causar ReDoS
- Sin sanitización de nombres de archivo

**Recomendaciones:**
- Validar extensiones de archivo
- Limitar tamaño de archivos
- Sanitizar entradas de usuario
- Agregar manejo de excepciones robusto

---

## 12. Escalabilidad

### 12.1 Limitaciones de Escalabilidad

**Número de Archivos:**
- Diseñado para: 1-50 archivos
- Práctico hasta: ~20 archivos
- Problemas con: 100+ archivos

**Tamaño de Archivos:**
- Diseñado para: Documentos típicos (< 5MB)
- Práctico hasta: 10MB por archivo
- Problemas con: Archivos de 50MB+

**Concurrencia:**
- Sin soporte de multi-threading
- Operaciones bloqueantes en UI
- No hay paralelización

### 12.2 Mejoras para Escalabilidad

**Sugerencias:**
- Implementar carga asíncrona
- Procesar archivos en background
- Agregar barra de progreso
- Implementar paginación de documentos
- Lazy loading (cargar bajo demanda)

---

## 13. Mantenibilidad

### 13.1 Calidad del Código

**Aspectos Positivos:**
- Nombres de variables descriptivos
- Estructura clara de métodos
- Separación de concerns (relativa)

**Aspectos a Mejorar:**
- Falta documentación (docstrings)
- Sin type hints
- Métodos largos (replace_text_selective)
- Lógica compleja sin comentarios

### 13.2 Testing

**Estado Actual:**
- Sin unit tests
- Sin integration tests
- Solo testing manual

**Dificultades para Testing:**
- Acoplamiento UI-lógica
- Sin inversión de dependencias
- Difícil moclear componentes

### 13.3 Refactoring Sugerido

**Mejoras recomendadas:**

1. **Separar lógica de UI:**
```python
class DocumentManager:
    def load_document(path)
    def search_text(text)
    def replace_text(old, new)
    
class WordEditorUI(ctk.CTk):
    def __init__():
        self.manager = DocumentManager()
```

2. **Agregar type hints:**
```python
def load_word(self) -> None:
    path: str = filedialog.askopenfilename()
```

3. **Documentación:**
```python
def replace_text_selective(self) -> None:
    """
    Reemplaza texto de forma selectiva pidiendo confirmación.
    
    Muestra un diálogo para cada coincidencia encontrada.
    El usuario puede aceptar o rechazar cada reemplazo.
    """
```

---

## 14. Conclusiones

### 14.1 Fortalezas de la Arquitectura
- Simplicidad: Fácil de entender
- Standalone: No requiere instalaciones adicionales ya que viene con exe
- Directo: Mínima abstracción
- Funcional: Cumple con los requisitos básicos

### 14.2 Debilidades de la Arquitectura
- Monolítica: Todo en una clase
- Acoplamiento alto: UI y lógica mezcladas
- Sin testing: Difícil de probar automáticamente
- Escalabilidad limitada: Problemas con muchos archivos

### 14.3 Recomendaciones para Futuras Versiones
1. Refactorizar en múltiples clases
2. Implementar patrón MVC apropiado
3. Agregar capa de abstracción para persistencia
4. Implementar unit tests
5. Agregar logging y manejo de errores robusto
6. Implementar procesamiento asíncrono
7. Mejorar gestión de memoria (historial limitado)

---

## 15. Glosario Técnico

| Término | Definición |
|---------|------------|
| **CustomTkinter** | Framework GUI moderno basado en Tkinter |
| **python-docx** | Librería para manipular archivos .docx |
| **Deep Copy** | Clonación completa e independiente de objetos |
| **Regex** | Regular Expressions - patrones de búsqueda |
| **Widget** | Componente de interfaz gráfica (botón, entrada, etc.) |
| **Callback** | Función ejecutada en respuesta a un evento |
| **Memento** | Patrón de diseño para guardar/restaurar estado |
| **Monolítico** | Arquitectura donde todo está en un solo componente |

---

## 16. Referencias

- Documentación CustomTkinter: https://customtkinter.tomschimansky.com/
- Documentación python-docx: https://python-docx.readthedocs.io/
- Código fuente: `/src/word_editor_massive.py`
- Manual de Usuario: `/docs/03-documentacion-tecnica/manual-usuario.md`

---

**Versión del Documento:** 1.0  
**Última Actualización:** 22/10/2025  
**Autor:** Rosa QA  
**Estado:** Completo

---

