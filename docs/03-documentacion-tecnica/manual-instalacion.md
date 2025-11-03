# Manual de Instalación - Editor Word Masivo

## Información del Documento

| Campo | Detalle |
|-------|---------|
| **Proyecto** | Editor Word Masivo v1.0 |
| **Documento** | Manual de Instalación |
| **Versión** | 1.0 |
| **Fecha** | 22/10/2025 |
| **Autor** | Rosa QA |

---

## 1. Introducción

### 1.1 Propósito
Este documento proporciona instrucciones detalladas para instalar y configurar la aplicación Editor Word Masivo en diferentes escenarios.

### 1.2 Audiencia
- Testers QA que necesitan configurar entorno de pruebas
- Usuarios finales que desean usar la aplicación
- Desarrolladores que trabajarán en el proyecto

### 1.3 Requisitos Previos
Conocimientos básicos de:
- Navegación en el sistema de archivos
- Uso de la terminal/línea de comandos (opcional)
- Instalación de software en Windows

---

## 2. Métodos de Instalación

Existen dos métodos para ejecutar la aplicación:

| Método | Complejidad | Requiere Python | Ventajas |
|--------|-------------|-----------------|----------|
| **Ejecutable (.exe)** | Baja | No | Rápido, no requiere instalaciones |
| **Código Fuente** | Media | Sí | Modificable, multiplataforma |

---

## 3. Instalación Método 1: Ejecutable (RECOMENDADO)

### 3.1 Requisitos del Sistema

**Sistema Operativo:**
- Windows 10 (64-bit) o superior
- Windows 11 (64-bit)

**Hardware Mínimo:**
- Procesador: Intel Core i3 o equivalente
- RAM: 4 GB
- Espacio en disco: 100 MB libres
- Resolución: 1280x720 o superior

**Hardware Recomendado:**
- Procesador: Intel Core i5 o superior
- RAM: 8 GB
- Espacio en disco: 500 MB libres
- Resolución: 1920x1080 (Full HD)

**Software:**
- No requiere Microsoft Word instalado
- No requiere Python
- No requiere dependencias adicionales

---

### 3.2 Pasos de Instalación

#### Paso 1: Descargar el Ejecutable

1. Navega a la carpeta `/releases/` del repositorio
2. Localiza el archivo: `EditorWordMasivo.exe`
3. Descarga el archivo a una ubicación de tu elección

**Ubicaciones recomendadas:**
- `C:\Program Files\EditorWordMasivo\`
- `C:\Users\[TuUsuario]\Documents\EditorWordMasivo\`
- Escritorio (para acceso rápido)

#### Paso 2: Verificar el Archivo

**Tamaño esperado:** Aproximadamente 30-50 MB

**Verificar integridad (opcional):**
```
Clic derecho en el archivo → Propiedades
Revisar tamaño y fecha de modificación
```

#### Paso 3: Desbloquear el Archivo (si es necesario)

Windows puede bloquear archivos descargados de internet:

1. Clic derecho en `EditorWordMasivo.exe`
2. Seleccionar **Propiedades**
3. En la pestaña **General**, buscar sección **Seguridad**
4. Marcar casilla **Desbloquear**
5. Click **Aplicar** → **Aceptar**

#### Paso 4: Ejecutar la Aplicación

**Primera ejecución:**

1. Doble clic en `EditorWordMasivo.exe`

2. Si aparece **Windows SmartScreen**:
   ```
   Windows protegió su PC
   Microsoft Defender SmartScreen impidió el inicio de una aplicación no reconocida
   ```
   
   **Solución:**
   - Click en **Más información**
   - Click en **Ejecutar de todas formas**
   - (Esto es normal para aplicaciones no firmadas digitalmente)

3. La aplicación se abrirá inmediatamente

#### Paso 5: Verificar Instalación Correcta

**La ventana debe mostrar:**
- Título: "Editor Word Masivo"
- Botones: Cargar Word, Cargar Varios Word
- Campos: Buscar..., Reemplazar por...
- Área de texto grande en la parte inferior
- Dimensiones: 900x600 píxeles

**Prueba básica:**
1. Click en "Cargar Word"
2. Seleccionar un archivo .docx
3. Verificar que el contenido se muestra

---

### 3.3 Crear Acceso Directo (Opcional)

**Para el Escritorio:**

1. Clic derecho en `EditorWordMasivo.exe`
2. Seleccionar **Enviar a** → **Escritorio (crear acceso directo)**

**Para el Menú Inicio:**

1. Clic derecho en `EditorWordMasivo.exe`
2. Seleccionar **Anclar al menú Inicio**

**Para la Barra de Tareas:**

1. Ejecutar la aplicación
2. Clic derecho en el icono de la barra de tareas
3. Seleccionar **Anclar a la barra de tareas**

---

### 3.4 Solución de Problemas Comunes

#### Problema 1: "No se puede abrir el archivo"

**Síntomas:**
- Doble clic no hace nada
- Mensaje de error al abrir

**Soluciones:**
1. Verificar que el archivo no está corrupto (re-descargar)
2. Desbloquear el archivo (ver Paso 3)
3. Ejecutar como administrador:
   - Clic derecho → **Ejecutar como administrador**

#### Problema 2: "Windows SmartScreen bloqueó permanentemente"

**Soluciones:**
1. Desbloquear en Propiedades (ver Paso 3)
2. Agregar excepción en Windows Defender:
   - Abrir **Seguridad de Windows**
   - **Protección contra virus y amenazas**
   - **Configuración de protección**
   - **Agregar o quitar exclusiones**
   - Agregar la carpeta del ejecutable

#### Problema 3: "La aplicación se cierra inmediatamente"

**Posibles causas:**
- Falta de permisos
- Conflicto con antivirus
- Sistema operativo incompatible

**Soluciones:**
1. Ejecutar como administrador
2. Desactivar temporalmente el antivirus
3. Verificar que Windows sea 64-bit:
   - Inicio → Configuración → Sistema → Acerca de
   - Revisar "Tipo de sistema"

#### Problema 4: "Error de DLL faltante"

**Mensaje:** "No se puede iniciar el programa porque falta VCRUNTIME140.dll"

**Solución:**
Instalar Microsoft Visual C++ Redistributable:
1. Ir a: https://aka.ms/vs/17/release/vc_redist.x64.exe
2. Descargar e instalar
3. Reiniciar la computadora
4. Intentar ejecutar la aplicación nuevamente

---

## 4. Instalación Método 2: Código Fuente

### 4.1 Requisitos Previos

**Software Necesario:**

1. **Python 3.8 o superior**
   - Recomendado: Python 3.13
   - Descargar de: https://www.python.org/downloads/

2. **pip (gestor de paquetes)**
   - Incluido con Python 3.4+
   - Verificar instalación: `pip --version`

3. **Git (opcional)**
   - Para clonar el repositorio
   - Descargar de: https://git-scm.com/downloads

---

### 4.2 Instalación de Python

#### Paso 1: Descargar Python

1. Ir a https://www.python.org/downloads/
2. Click en "Download Python 3.13.x"
3. Ejecutar el instalador descargado

#### Paso 2: Instalar Python

**IMPORTANTE:** Durante la instalación:

1. Marcar casilla: **"Add Python to PATH"** (CRÍTICO)
2. Seleccionar **"Install Now"** o **"Customize installation"**
3. Si customizas:
   - Marcar todas las opciones
   - En "Advanced Options", marcar:
     - Install for all users
     - Add Python to environment variables
4. Click **Install**
5. Esperar a que finalice
6. Click **Close**

#### Paso 3: Verificar Instalación

Abrir **Símbolo del sistema** (CMD) o **PowerShell**:

```bash
python --version
```

**Salida esperada:**
```
Python 3.13.0
```

```bash
pip --version
```

**Salida esperada:**
```
pip 23.x.x from C:\...\Python\...
```

**Si no funciona:**
- Reiniciar la computadora
- Verificar que Python está en PATH
- Re-instalar Python marcando "Add to PATH"

---

### 4.3 Obtener el Código Fuente

#### Opción A: Clonar con Git

```bash
# Navegar a carpeta deseada
cd C:\Users\[TuUsuario]\Documents

# Clonar repositorio
git clone https://github.com/[usuario]/word-editor-qa-portfolio.git

# Entrar a la carpeta
cd word-editor-qa-portfolio
```

#### Opción B: Descargar ZIP

1. Ir al repositorio en GitHub
2. Click en **Code** → **Download ZIP**
3. Extraer el archivo ZIP
4. Navegar a la carpeta extraída

---

### 4.4 Instalar Dependencias

#### Paso 1: Abrir Terminal en la Carpeta del Proyecto

**Método 1 (Windows Explorer):**
1. Abrir la carpeta del proyecto
2. Shift + Clic derecho en espacio vacío
3. Seleccionar **"Abrir ventana de PowerShell aquí"**

**Método 2 (CMD):**
```bash
cd C:\ruta\al\proyecto\word-editor-qa-portfolio
```

#### Paso 2: Crear Entorno Virtual (Recomendado)

**¿Por qué?** Aisla las dependencias del proyecto

```bash
# Crear entorno virtual
python -m venv venv

# Activar entorno virtual
# En Windows CMD:
venv\Scripts\activate.bat

# En Windows PowerShell:
venv\Scripts\Activate.ps1

# En Git Bash:
source venv/Scripts/activate
```

**Salida esperada:**
```
(venv) C:\ruta\al\proyecto>
```

El `(venv)` indica que el entorno está activo.

#### Paso 3: Instalar Librerías

**Opción A: Usando requirements.txt (si existe)**

```bash
pip install -r requirements.txt
```

**Opción B: Instalar manualmente**

```bash
pip install customtkinter
pip install python-docx
pip install fpdf
```

**Verificar instalación:**
```bash
pip list
```

**Salida esperada (parcial):**
```
Package          Version
---------------- -------
customtkinter    5.2.0
python-docx      1.1.0
fpdf             1.7.2
...
```

#### Paso 4: Verificar Instalación de Dependencias

Crear archivo `test_imports.py`:

```python
try:
    import customtkinter
    print("✓ customtkinter instalado")
except:
    print("✗ customtkinter NO instalado")

try:
    from docx import Document
    print("✓ python-docx instalado")
except:
    print("✗ python-docx NO instalado")

try:
    from fpdf import FPDF
    print("✓ fpdf instalado")
except:
    print("✗ fpdf NO instalado")
```

Ejecutar:
```bash
python test_imports.py
```

**Salida esperada:**
```
✓ customtkinter instalado
✓ python-docx instalado
✓ fpdf instalado
```

---

### 4.5 Ejecutar la Aplicación

#### Método 1: Desde la Terminal

```bash
# Asegurarse de estar en la carpeta del proyecto
cd word-editor-qa-portfolio

# Ejecutar
python src/word_editor_massive.py
```

#### Método 2: Desde un IDE

**Visual Studio Code:**
1. Abrir carpeta del proyecto
2. Abrir archivo `src/word_editor_massive.py`
3. Presionar F5 o click en "Run"

**PyCharm:**
1. Open Project → Seleccionar carpeta
2. Abrir `src/word_editor_massive.py`
3. Click derecho → Run

**IDLE (incluido con Python):**
1. Abrir IDLE
2. File → Open → `word_editor_massive.py`
3. Run → Run Module (F5)

#### Método 3: Crear Script de Inicio

**Windows (run.bat):**
```batch
@echo off
cd /d "%~dp0"
call venv\Scripts\activate.bat
python src\word_editor_massive.py
pause
```

Guardar como `run.bat` en la raíz del proyecto.
Doble clic para ejecutar.

---

### 4.6 Solución de Problemas (Código Fuente)

#### Problema 1: "Python no se reconoce como comando"

**Causa:** Python no está en PATH

**Solución:**
1. Re-instalar Python marcando "Add to PATH"
2. O agregar manualmente:
   - Inicio → Variables de entorno
   - PATH → Editar
   - Agregar: `C:\Python313\` y `C:\Python313\Scripts\`

#### Problema 2: "ModuleNotFoundError: No module named 'customtkinter'"

**Causa:** Dependencias no instaladas o entorno virtual no activado

**Solución:**
```bash
# Activar entorno virtual
venv\Scripts\activate

# Instalar dependencia
pip install customtkinter
```

#### Problema 3: "pip no se reconoce como comando"

**Causa:** pip no instalado o no en PATH

**Solución:**
```bash
# Verificar instalación de pip
python -m pip --version

# Si funciona, usar:
python -m pip install customtkinter
```

#### Problema 4: "_tkinter.TclError: Can't find a usable init.tcl"

**Causa:** Problema con instalación de Tkinter

**Solución:**
1. Re-instalar Python
2. Asegurarse de instalar "tcl/tk and IDLE"
3. O usar instalador "full" de Python

#### Problema 5: "PermissionError: [Errno 13]"

**Causa:** Sin permisos para escribir en carpeta

**Solución:**
1. Ejecutar terminal como administrador
2. O mover proyecto a carpeta con permisos

---

## 5. Creación de Ejecutable (Opcional)

### 5.1 ¿Por qué crear un ejecutable?

**Ventajas:**
- No requiere Python instalado
- Más fácil de distribuir
- Ejecutable con un doble clic
- Empaqueta todas las dependencias

**Desventajas:**
- Archivo grande (30-50 MB)
- Tiempo de compilación
- Solo funciona en Windows

---

### 5.2 Usar PyInstaller

#### Paso 1: Instalar PyInstaller

```bash
pip install pyinstaller
```

#### Paso 2: Crear Ejecutable

**Comando básico:**
```bash
pyinstaller --onefile --windowed src/word_editor_massive.py
```

**Comando con opciones:**
```bash
pyinstaller --onefile ^
            --windowed ^
            --name "EditorWordMasivo" ^
            --icon=icon.ico ^
            src/word_editor_massive.py
```

**Explicación de opciones:**
- `--onefile`: Crea un solo archivo .exe
- `--windowed`: Sin ventana de consola
- `--name`: Nombre del ejecutable
- `--icon`: Icono personalizado (opcional)

#### Paso 3: Localizar el Ejecutable

```
dist/
└── EditorWordMasivo.exe
```

El archivo está en la carpeta `dist/`

#### Paso 4: Probar el Ejecutable

1. Navegar a `dist/`
2. Doble clic en `EditorWordMasivo.exe`
3. Verificar que funciona correctamente

---

### 5.3 Solución de Problemas (PyInstaller)

#### Problema: "Failed to execute script"

**Solución:**
Ejecutar sin `--windowed` para ver errores:
```bash
pyinstaller --onefile src/word_editor_massive.py
```

#### Problema: "ModuleNotFoundError en el ejecutable"

**Solución:**
Agregar imports ocultos:
```bash
pyinstaller --onefile ^
            --hidden-import=customtkinter ^
            --hidden-import=docx ^
            src/word_editor_massive.py
```

---

## 6. Configuración del Entorno de Testing

### 6.1 Configuración para QA

**Estructura recomendada:**

```
C:\QA_Testing\
├── EditorWordMasivo.exe
├── test-data\
│   ├── documento-pequeño.docx
│   ├── documento-mediano.docx
│   └── documento-grande.docx
└── evidencias\
    ├── screenshots\
    └── videos\
```

### 6.2 Preparar Datos de Prueba

**Crear archivos de prueba:**

1. **documento-pequeño.docx** (1 página)
   - Texto simple con 3-5 párrafos
   - Incluir palabras repetidas para buscar

2. **documento-mediano.docx** (10 páginas)
   - Texto con varios párrafos
   - Incluir errores ortográficos intencionales

3. **documento-grande.docx** (50+ páginas)
   - Para pruebas de rendimiento
   - Texto repetitivo

### 6.3 Instalar Herramientas de Captura

**ShareX (recomendado):**
1. Descargar de: https://getsharex.com/
2. Instalar
3. Configurar tecla de captura (F12)

**OBS Studio (para videos):**
1. Descargar de: https://obsproject.com/
2. Instalar
3. Configurar fuente de captura

---

## 7. Desinstalación

### 7.1 Desinstalar Ejecutable

**Método simple:**
1. Eliminar el archivo `EditorWordMasivo.exe`
2. Eliminar accesos directos creados
3. No requiere desinstalador

**Método completo:**
1. Eliminar carpeta de instalación
2. Eliminar datos de usuario (si existen)
3. Limpiar registro (opcional)

### 7.2 Desinstalar Código Fuente

```bash
# Desactivar entorno virtual
deactivate

# Eliminar carpeta del proyecto
rmdir /s word-editor-qa-portfolio
```

### 7.3 Desinstalar Python (si es necesario)

1. Inicio → Configuración → Aplicaciones
2. Buscar "Python 3.13"
3. Click → Desinstalar
4. Seguir asistente

---

## 8. Verificación Post-Instalación

### 8.1 Checklist de Verificación

- [ ] La aplicación se abre sin errores
- [ ] Se pueden cargar archivos .docx
- [ ] El contenido se muestra correctamente
- [ ] La función de búsqueda funciona
- [ ] La función de reemplazo funciona
- [ ] Se pueden guardar archivos
- [ ] No hay errores en consola (si se ejecuta desde Python)

### 8.2 Prueba Funcional Básica

**Test rápido (2 minutos):**

1. Abrir la aplicación
2. Click "Cargar Word"
3. Seleccionar un archivo .docx
4. Verificar contenido visible
5. Escribir "test" en "Buscar..."
6. Verificar resaltado amarillo
7. Escribir "prueba" en "Reemplazar por..."
8. Click "Reemplazar Todo"
9. Click "Guardar Como"
10. Seleccionar carpeta y guardar

**Resultado esperado:** Todo funciona sin errores

---

## 9. Recursos Adicionales

### 9.1 Enlaces Útiles

- Repositorio del proyecto: [URL del repo]
- Documentación de Python: https://docs.python.org/3/
- Documentación de CustomTkinter: https://customtkinter.tomschimansky.com/
- Reportar bugs: [URL de issues]

### 9.2 Soporte

**Para problemas de instalación:**
- Revisar este manual completo
- Verificar requisitos del sistema
- Consultar sección de solución de problemas

**Para reportar bugs:**
- Usar plantilla en `/bug-reports/template-bug-report.md`
- Incluir pasos para reproducir
- Adjuntar capturas de pantalla

---

## 10. Preguntas Frecuentes (FAQ)

**P: ¿Necesito Microsoft Word instalado?**
R: No, la aplicación es independiente de Microsoft Word.

**P: ¿Funciona en macOS o Linux?**
R: El ejecutable solo funciona en Windows. El código fuente puede ejecutarse en cualquier plataforma con Python.

**P: ¿Puedo usar archivos .doc (Word antiguo)?**
R: No, solo soporta .docx (Word 2007+).

**P: ¿Cuántos archivos puedo cargar a la vez?**
R: Recomendado hasta 20 archivos. Práctico hasta 50.

**P: ¿Los cambios se guardan automáticamente?**
R: No, debes hacer clic en "Guardar Como" para persistir los cambios.

**P: ¿Se pierden el formato del documento?**
R: Sí, solo se preserva el texto plano. Se pierde negrita, cursiva, tablas, etc.

---

## 11. Glosario

| Término | Definición |
|---------|------------|
| **Ejecutable** | Archivo .exe que se puede ejecutar sin instalaciones |
| **Dependencia** | Librería requerida por la aplicación |
| **Entorno Virtual** | Espacio aislado para instalar dependencias de Python |
| **PATH** | Variable de entorno que indica dónde buscar ejecutables |
| **pip** | Gestor de paquetes de Python |
| **PyInstaller** | Herramienta para crear ejecutables desde Python |

---

## 12. Historial de Versiones

| Versión | Fecha | Cambios |
|---------|-------|---------|
| 1.0 | 22/10/2025 | Creación inicial del manual |

---

**Autor:** Rosa QA  
**Última Actualización:** 22/10/2025  
**Estado:** Completo

---