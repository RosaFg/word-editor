BUG-001: Reemplazo Selectivo No Aplica Cambios Correctamente en Múltiples Coincidencias
📋 Información General

ID: BUG-001
Fecha de Reporte: 22/10/2025
Reportado por: QA Tester
Módulo Afectado: Reemplazo de Texto (Función replace_text_selective)
Versión: v1.0
Estado: 🔴 Abierto
Archivo de Código: word_editor_massive.py, línea 123-146

🎯 Severidad y Prioridad

Severidad: 🟡 Media

Afecta funcionalidad principal pero tiene workaround
No causa pérdida de datos
Usuario puede usar "Reemplazar Todo" como alternativa


Prioridad: 🟡 Media

Debe corregirse en próxima versión
Afecta experiencia de usuario


📝 Descripción
Al utilizar la función "Reemplazar" (reemplazo selectivo) para buscar y reemplazar texto, cuando existen múltiples coincidencias en el mismo párrafo, solo se aplica correctamente el primer reemplazo. Los reemplazos posteriores en el mismo párrafo fallan o reemplazan texto incorrecto debido a que los índices de posición se invalidan después del primer cambio.
Ejemplo del problema:
Texto original: "El cliente contactó al cliente principal"
Buscar: "cliente"
Reemplazar por: "comprador"

Resultado esperado: "El comprador contactó al comprador principal"
Resultado obtenido: "El comprador contactó al cliente principal" 
                     ó texto corrupto/incorrecto
🔄 Pasos para Reproducir
Precondiciones:

Tener un archivo .docx con un párrafo que contenga múltiples instancias de la misma palabra

Pasos:

Abrir la aplicación EditorWordMasivo.exe
Hacer clic en "Cargar Word"
Seleccionar un documento con el siguiente contenido:

   El cliente visitó la tienda. El cliente está satisfecho con el servicio al cliente.

En el campo "Buscar..." escribir: cliente
En el campo "Reemplazar por..." escribir: comprador
Hacer clic en el botón "Reemplazar"
En el diálogo de confirmación para la primera coincidencia:

Click en "Sí" para reemplazar


En el diálogo de confirmación para la segunda coincidencia:

Click en "Sí" para reemplazar


En el diálogo de confirmación para la tercera coincidencia:

Click en "Sí" para reemplazar


Revisar el texto resultante en el área de texto

✅ Resultado Esperado
El comprador visitó la tienda. El comprador está satisfecho con el servicio al comprador.
Todas las instancias de "cliente" deberían ser reemplazadas por "comprador".
❌ Resultado Actual
El comprador visitó la tienda. El comprador está satisfecho con el servicio al cliente.
O en algunos casos:
El comprador visitó la tienda. El cliente está satisfecho con el servicio al cliente.
Observación: Solo el primer reemplazo se aplica correctamente. Los siguientes reemplazos en el mismo párrafo fallan o no se ejecutan.
🔍 Análisis Técnico del Bug
Causa Raíz:
El código actual en la línea 143-145:
pythonif answer:
    para = doc.paragraphs[p_idx]
    para.text = para.text[:start] + replace_text + para.text[end:]
Problema identificado:

El código almacena las posiciones (start, end) de todas las coincidencias al inicio
Cuando se realiza el primer reemplazo, el texto del párrafo cambia
Los índices start y end de las coincidencias posteriores ya no son válidos
Si "cliente" (7 caracteres) se reemplaza por "comprador" (9 caracteres), se añaden 2 caracteres
La segunda coincidencia que estaba en la posición 35, ahora está en la posición 37
El código intenta reemplazar usando la posición 35 (incorrecta), causando:

Reemplazo en la ubicación equivocada
Texto corrupto
Reemplazo no aplicado



Código Problemático:
python# Línea 132-135: Se guardan TODAS las posiciones de una vez
matches = []
for i, para in enumerate(doc.paragraphs):
    for m in pattern.finditer(para.text):
        matches.append((i, m.start(), m.end(), para.text[m.start():m.end()]))

# Línea 141-145: Se usan las posiciones guardadas (que ya están obsoletas)
for idx, (p_idx, start, end, text) in enumerate(matches, start=1):
    answer = messagebox.askyesno("Reemplazar coincidencia", f"Reemplazar '{text}' en el párrafo {p_idx+1}?")
    if answer:
        para = doc.paragraphs[p_idx]
        para.text = para.text[:start] + replace_text + para.text[end:]  # ❌ Índices obsoletos
🖼️ Evidencias
Screenshot 1: Estado Inicial
[CAPTURA RECOMENDADA]
- Mostrar documento con: "El cliente visitó al cliente"
- Campo "Buscar..." con: "cliente"
- Campo "Reemplazar por..." con: "comprador"
Screenshot 2: Primer Diálogo de Confirmación
[CAPTURA RECOMENDADA]
- Diálogo preguntando: "¿Reemplazar 'cliente' en el párrafo 1?"
- Botones: [Sí] [No]
Screenshot 3: Resultado Incorrecto
[CAPTURA RECOMENDADA]
- Texto resultante mostrando solo un reemplazo aplicado
- Resaltado en amarillo de las palabras no reemplazadas
Log de Consola:
(No hay errores en consola - el bug es lógico, no de excepción)
🔧 Entorno

Sistema Operativo: Windows 11 Pro
Versión de Python: 3.11.x (compilado en .exe)
Dependencias:

customtkinter: v5.2.0
python-docx: v1.1.0


Tamaño del archivo de prueba: 12 KB
Número de párrafos: 1
Coincidencias en el texto: 3 instancias de "cliente"

💡 Solución Propuesta
Opción 1: Recalcular posiciones después de cada reemplazo
pythondef replace_text_selective(self):
    # ... código inicial igual ...
    
    self.history.append(copy.deepcopy(self.docs))
    doc = self.docs[self.current_index]
    
    # En lugar de guardar todas las coincidencias, buscar una a una
    while True:
        # Buscar la PRIMERA coincidencia en el texto actual
        found = False
        for i, para in enumerate(doc.paragraphs):
            match = pattern.search(para.text)
            if match:
                found = True
                answer = messagebox.askyesno(
                    "Reemplazar coincidencia", 
                    f"¿Reemplazar '{match.group()}' en el párrafo {i+1}?"
                )
                if answer:
                    # Reemplazar SOLO esta coincidencia
                    para.text = para.text[:match.start()] + replace_text + para.text[match.end():]
                    self.update_text_area()
                break  # Salir del for para buscar de nuevo desde el inicio
        
        if not found:
            break  # No hay más coincidencias
    
    messagebox.showinfo("Reemplazo", "Reemplazo selectivo completado.")
Opción 2: Usar regex.sub con función callback
pythondef replace_text_selective(self):
    # ... código inicial igual ...
    
    replacements = []
    
    # Primero, preguntar por cada coincidencia
    for i, para in enumerate(doc.paragraphs):
        for match in pattern.finditer(para.text):
            answer = messagebox.askyesno(
                "Reemplazar coincidencia",
                f"¿Reemplazar '{match.group()}' en el párrafo {i+1}?"
            )
            replacements.append((i, match.start(), match.end(), answer))
    
    # Luego aplicar los cambios de atrás hacia adelante (para mantener índices)
    for i, start, end, do_replace in reversed(replacements):
        if do_replace:
            para = doc.paragraphs[i]
            para.text = para.text[:start] + replace_text + para.text[end:]
✅ Opción Recomendada: Opción 1

Más simple y menos propensa a errores
El usuario ve los cambios en tiempo real
Evita problemas de índices obsoletos

📌 Workaround (Solución Temporal)
Mientras se corrige el bug, los usuarios pueden:

Usar "Reemplazar Todo" si están seguros del cambio
Reemplazar de uno en uno manualmente:

Buscar el término
Ver las coincidencias resaltadas
Editar manualmente en el área de texto


Hacer múltiples pasadas:

Ejecutar "Reemplazar" varias veces
En cada pasada reemplazar solo la primera coincidencia
Repetir hasta que no haya más coincidencias



📊 Impacto
Usuarios Afectados:

✅ Todos los usuarios que utilicen la función "Reemplazar" (selectivo)
❌ NO afecta a usuarios que usen solo "Reemplazar Todo"

Frecuencia:

🔴 Alta - Ocurre cada vez que hay múltiples coincidencias en un mismo párrafo

Casos de Uso Afectados:

Corrección selectiva de errores ortográficos
Actualización parcial de términos
Revisión manual de cambios antes de aplicar

🔗 Relación con Otros Bugs

Relacionado con: BUG-002 (Historial de deshacer puede no reflejar todos los cambios)
Bloqueado por: Ninguno
Bloquea: Ninguno

📝 Notas Adicionales

Este bug NO afecta la función "Reemplazar Todo" (línea 148-163)
El bug existe desde la versión 1.0 (primera release)
Se recomienda agregar tests unitarios para verificar la corrección
Considerar agregar un modo "Vista Previa" antes de aplicar cambios