2.5 Archivos para Pruebas Negativas
2.5.1 corrupto.docx
Propósito: Verificar manejo de archivos corruptos
Creación: Tomar un .docx válido y modificar bytes aleatorios con editor hexadecimal
Casos de prueba asociados: TC-010
Resultado esperado:

Mensaje de error al intentar cargar
La aplicación NO se cierra (no crash)
El mensaje es claro para el usuario


2.5.2 documento.doc
Propósito: Verificar rechazo de formato Word antiguo
Tipo: Microsoft Word 97-2003 (.doc)
Casos de prueba asociados: TC-010
Resultado esperado:

No aparece en el diálogo (filtro activo)
O muestra error si se intenta forzar carga


2.5.3 documento.pdf
Propósito: Verificar rechazo de PDF
Tipo: Archivo PDF válido
Casos de prueba asociados: TC-010
Resultado esperado:

No se puede seleccionar en el diálogo
No se carga aunque se intente


2.5.4 documento.txt
Propósito: Verificar rechazo de texto plano
Tipo: Archivo de texto plano (.txt)
Casos de prueba asociados: TC-010
Resultado esperado:

No aparece en el diálogo de selección
No se carga si se intenta forzar