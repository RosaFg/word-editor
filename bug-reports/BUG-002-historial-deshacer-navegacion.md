BUG-002: Historial de Deshacer se Pierde al Navegar Entre Documentos
📋 Información General

ID: BUG-002
Fecha de Reporte: 22/10/2025
Reportado por: QA Tester
Módulo Afectado: Gestión de Historial (Función undo)
Versión: v1.0
Estado: 🔴 Abierto
Archivo de Código: word_editor_massive.py, línea 165-172

🎯 Severidad y Prioridad

Severidad: 🟢 Baja

No causa pérdida de datos permanente
Funcionalidad secundaria
Usuario puede prevenir el problema fácilmente


Prioridad: 🟢 Baja

Puede esperar a futuras versiones
Comportamiento puede documentarse como "esperado"



📝 Descripción
El historial de cambios para la función "Deshacer" se mantiene globalmente para todos los documentos cargados. Sin embargo, cuando el usuario navega entre documentos usando los botones "Anterior" y "Siguiente", el estado visual del documento puede no reflejar el historial guardado, causando confusión sobre qué cambios se deshicieron realmente.
Además, el historial NO es específico por documento, lo que significa que deshacer cambios puede afectar documentos diferentes al que se está visualizando actualmente.
🔄 Pasos para Reproducir
Precondiciones:

Tener 2 o más archivos .docx disponibles

Pasos:

Abrir la aplicación EditorWordMasivo.exe
Hacer clic en "Cargar Varios Word"
Seleccionar 2 archivos diferentes (por ejemplo: doc1.docx y doc2.docx)
Verificar que se muestra el primer documento (doc1.docx)
En "Buscar..." escribir una palabra que exista en doc1
En "Reemplazar por..." escribir un texto diferente
Hacer clic en "Reemplazar Todo"
✅ Verificar que el texto cambió en doc1
Hacer clic en botón "Siguiente >>" para ver doc2
Verificar que se muestra doc2 (sin cambios, como se espera)
Hacer clic en "Deshacer"
Observar el mensaje: "Cambio deshecho"
Hacer clic en "<< Anterior" para volver a doc1
Observar el documento doc1

✅ Resultado Esperado
Opción A (comportamiento ideal):

Al hacer clic en "Deshacer" mientras se ve doc2, el sistema debe indicar: "No hay cambios para deshacer en este documento"
El historial debe ser independiente por documento

Opción B (comportamiento aceptable):

Al hacer clic en "Deshacer", el sistema debe:

Deshacer el último cambio (de doc1)
Cambiar automáticamente la vista a doc1
Mostrar: "Cambio deshecho en documento 1"



❌ Resultado Actual

Al hacer clic en "Deshacer" mientras se visualiza doc2:

✅ Muestra mensaje: "Cambio deshecho"
❌ Sigue mostrando doc2 (sin cambios visibles)
❌ No indica que se deshizo un cambio en otro documento


Al volver a doc1:

✅ Los cambios están deshecho (funciona correctamente)
❌ El usuario no recibió feedback visual inmediato



Problema de UX: El usuario no sabe que deshizo cambios en un documento diferente al que está viendo.
🔍 Análisis Técnico del Bug
Causa Raíz:

La variable self.history es una lista única para TODOS los documentos
La función undo() no actualiza current_index ni llama a update_text_area() después de deshacer
No hay verificación de qué documento fue modificado en el historial

Código Problemático:
python# Línea 165-172
def undo(self):
    if len(self.history) > 1:
        self.history.pop()
        self.docs = copy.deepcopy(self.history[-1])  # ✅ Deshace cambio
        self.update_text_area()  # ✅ Actualiza vista
        messagebox.showinfo("Deshacer", "Cambio deshecho.")  # ⚠️ Mensaje genérico
    else:
        messagebox.showinfo("Deshacer", "No hay cambios para deshacer.")
Limitaciones:

✅ La función update_text_area() actualiza el documento actual (current_index)
❌ Pero si el cambio fue en otro documento, el usuario no lo ve inmediatamente
❌ El mensaje no indica en qué documento se deshizo el cambio

🖼️ Evidencias
Screenshot 1: Antes de Deshacer
[CAPTURA RECOMENDADA]
- Vista de doc2.docx (sin cambios)
- Etiqueta: "Archivo 2/2: doc2.docx"
- Botón "Deshacer" habilitado
Screenshot 2: Después de Deshacer
[CAPTURA RECOMENDADA]
- Aún en vista de doc2.docx
- Mensaje: "Cambio deshecho"
- No hay cambios visibles (porque doc2 nunca se modificó)
Screenshot 3: Al Volver a doc1
[CAPTURA RECOMENDADA]
- Vista de doc1.docx
- Los cambios están deshecho (texto original restaurado)
- Esto demuestra que el "Deshacer" SÍ funcionó, pero en otro documento
🔧 Entorno

Sistema Operativo: Windows 11 Pro
Versión: v1.0
Documentos de prueba: 2 archivos .docx
Tamaño: 10-15 KB cada uno

💡 Solución Propuesta
Opción 1: Mejorar el mensaje de feedback
pythondef undo(self):
    if len(self.history) > 1:
        self.history.pop()
        self.docs = copy.deepcopy(self.history[-1])
        
        # Actualizar TODOS los documentos visualmente
        current_doc_name = os.path.basename(self.file_paths[self.current_index])
        self.update_text_area()
        
        messagebox.showinfo(
            "Deshacer", 
            f"Cambio deshecho.\nRevisando: {current_doc_name}\n\nSi el cambio fue en otro documento, navega para verlo."
        )
    else:
        messagebox.showinfo("Deshacer", "No hay cambios para deshacer.")
Opción 2: Historial por documento (más complejo)
pythondef __init__(self):
    # ...
    self.history = {}  # Diccionario: {doc_index: [estados]}
    
def undo(self):
    doc_idx = self.current_index
    if doc_idx in self.history and len(self.history[doc_idx]) > 1:
        self.history[doc_idx].pop()
        self.docs[doc_idx] = copy.deepcopy(self.history[doc_idx][-1])
        self.update_text_area()
        messagebox.showinfo("Deshacer", "Cambio deshecho en documento actual.")
    else:
        messagebox.showinfo("Deshacer", "No hay cambios para deshacer en este documento.")
✅ Opción Recomendada: Opción 1 (corto plazo) + Opción 2 (largo plazo)

Opción 1 es rápida de implementar y mejora la UX inmediatamente
Opción 2 requiere refactorización pero es la solución correcta

📌 Workaround (Solución Temporal)
Los usuarios pueden evitar confusión:

No navegar entre documentos después de hacer cambios, hasta guardar
Usar "Deshacer" inmediatamente después de cada cambio, antes de navegar
Verificar todos los documentos después de usar "Deshacer" para confirmar qué cambió

📊 Impacto
Usuarios Afectados:

✅ Solo usuarios que cargan múltiples archivos
✅ Solo cuando usan "Deshacer" después de navegar entre documentos

Frecuencia:

🟡 Media-Baja - Depende del flujo de trabajo del usuario

Casos de Uso Afectados:

Edición de múltiples documentos con correcciones iterativas
Usuarios que usan mucho la función "Deshacer"

🔗 Relación con Otros Bugs

Relacionado con: BUG-001 (el historial se usa en reemplazos selectivos)
Bloqueado por: Ninguno
Bloquea: Ninguno

📝 Notas Adicionales

Este comportamiento puede documentarse como "por diseño" si se considera que el historial global es intencional
La mayoría de usuarios probablemente usen la app con un solo documento a la vez
Agregar tooltips o ayuda contextual podría mitigar la confusión


Fin del Reporte de Bugs