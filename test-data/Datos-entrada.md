3. Datos de Entrada para Campos
3.1 Campo "Buscar..."
3.1.1 Valores Positivos (Válidos)
EntradaPropósitoResultado Esperado"cliente"Búsqueda normalResalta todas las coincidencias"Cliente"Búsqueda con mayúsculaResalta igual que "cliente" (case-insensitive)"el"Palabra cortaResalta todas las apariciones"producto"Palabra únicaResalta coincidencia exacta"El cliente"Frase con espacioResalta la frase completa"100"NúmeroResalta el número"$"SímboloResalta el símbolo monetario"á"Vocal acentuadaResalta la vocal acentuada"ñ"Letra ñResalta la letra ñ"?"Signo de puntuaciónResalta el signo
3.1.2 Valores Límite
EntradaPropósitoResultado Esperado"" (vacío)Campo vacíoNo resalta nada, no da error"a"Un solo carácterResalta todas las "a""xyz"Texto no existenteNo resalta nada, no da error"palabra muy larga que probablemente no existe en el documento"Texto largoNo resalta nada"   " (espacios)Solo espaciosPuede o no resaltar espacios
3.1.3 Valores Negativos (Para observar comportamiento)
EntradaPropósitoComportamiento Observado"@#$%"Caracteres especialesBusca literalmente estos caracteres"\n"Secuencia escapeBusca literalmente "\n""*"Asterisco (wildcard en regex)Busca literalmente "*" (escapado)"."Punto (any char en regex)Busca literalmente "." (escapado)

3.2 Campo "Reemplazar por..."
3.2.1 Valores Positivos
EntradaPropósitoResultado Esperado"comprador"Reemplazo normalReemplaza "cliente" por "comprador""Comprador"Con mayúsculaReemplaza manteniendo la mayúscula ingresada"nuevo texto"Frase con espacioReemplaza con la frase completa"200"NúmeroReemplaza con el número"" (vacío)Reemplazo por vacíoElimina el texto buscado"$200"Con símboloReemplaza incluyendo el símbolo
3.2.2 Valores Especiales
EntradaPropósitoResultado"XXXXX"Texto más largoReemplaza con texto más largo"X"Texto más cortoReemplaza con texto más corto"  " (espacios múltiples)Solo espaciosReemplaza con espacios

3.3 Combinaciones de Búsqueda y Reemplazo
3.3.1 Casos Comunes
BuscarReemplazar porCaso de Uso"recivir""recibir"Corrección ortográfica"Sr.""Señor"Expansión de abreviatura"Señor""Sr."Reducción a abreviatura"$100""$150"Actualización de precio"2024""2025"Actualización de año"correo@viejo.com""correo@nuevo.com"Cambio de email"  " (doble espacio)" " (espacio simple)Corrección de formato
3.3.2 Casos Especiales
BuscarReemplazar porPropósito"color""colour"Cambio de idioma (ES a EN)"10%""15%"Actualización de porcentaje"Capítulo 1""Capítulo I"Cambio de numeración"TODO:""HECHO:"Marcadores de estado

4. Datos para Pruebas de Guardado
4.1 Rutas de Guardado
4.1.1 Rutas Válidas
RutaPropósitoC:\test-results\Carpeta estándar de resultadosC:\Users[Usuario]\Documents\pruebas\Carpeta en DocumentosD:\respaldos\Unidad diferenteC:\temp\Carpeta temporal
4.1.2 Rutas con Casos Especiales
RutaCaso EspecialC:\test results\Ruta con espacio en nombreC:\test-ñ-á\Ruta con caracteres acentuadosC:\a\b\c\d\e\f\Ruta muy anidada

5. Datos para Navegación
5.1 Conjuntos de Archivos
5.1.1 Set Mínimo (2 archivos)
Uso: Probar navegación básica
Archivos:

archivo-a.docx
archivo-b.docx

5.1.2 Set Estándar (5 archivos)
Uso: Prueba normal de navegación
Archivos:

doc01.docx
doc02.docx
doc03.docx
doc04.docx
doc05.docx

5.1.3 Set Grande (20 archivos)
Uso: Prueba de rendimiento en navegación
Archivos: doc01.docx hasta doc20.docx

6. Matriz de Datos vs Casos de Prueba
Dato de PruebaTC-001TC-002TC-003TC-004TC-005TC-006TC-007TC-008TC-009TC-010documento-pequeno.docxXXXXdocumento-mediano.docxXXXXXdocumento-grande.docxXXSet 3 documentosXXreemplazo-selectivo.docxXSet reemplazo-masivoXdocumento-acentos.docxXXdocumento-vacio.docxXcorrupto.docxXdocumento.docXdocumento.pdfX

7. Instrucciones de Preparación
7.1 Crear Archivos de Prueba
Método 1: Manual

Abrir Microsoft Word
Copiar el contenido especificado
Guardar como .docx con el nombre indicado
Colocar en carpeta C:\test-data\

Método 2: Automatizado (Script)
python# Script para generar archivos de prueba
# (Código de ejemplo proporcionado por separado)
7.2 Organización de Carpetas
C:\test-data\
├── basicos\
│   ├── documento-pequeno.docx
│   ├── documento-mediano.docx
│   └── documento-grande.docx
│
├── carga-multiple\
│   ├── doc1.docx
│   ├── doc2.docx
│   └── doc3.docx
│
├── reemplazo\
│   ├── reemplazo-selectivo.docx
│   ├── archivo1.docx
│   └── archivo2.docx
│
├── especiales\
│   ├── documento-acentos.docx
│   ├── documento-saltos-linea.docx
│   └── documento-vacio.docx
│
└── negativos\
    ├── corrupto.docx
    ├── documento.doc
    ├── documento.pdf
    └── documento.txt

8. Validación de Datos de Prueba
8.1 Checklist de Validación
Antes de ejecutar las pruebas, verificar:

 Todos los archivos .docx se abren correctamente en Microsoft Word
 Los archivos contienen el contenido especificado
 Los tamaños de archivo son aproximadamente correctos
 Los archivos negativos están en el formato correcto (corruptos, .doc, etc.)
 Las carpetas de test-data están organizadas correctamente
 Se tienen permisos de lectura en todos los archivos
 Los nombres de archivo no tienen caracteres problemáticos

8.2 Verificación Rápida
Comando para contar archivos (PowerShell):
powershellGet-ChildItem -Path "C:\test-data" -Recurse -Filter "*.docx" | Measure-Object
Resultado esperado: Al menos 15 archivos .docx

9. Mantenimiento de Datos de Prueba
9.1 Actualización
Frecuencia: Cada nueva versión de la aplicación
Procedimiento:

Revisar si hay nuevos casos de prueba
Crear archivos adicionales si es necesario
Actualizar este documento
Versionar los cambios en Git

9.2 Respaldo
Ubicación de respaldo: C:\test-data-backup\
Frecuencia: Mensual o antes de cambios mayores

10. Notas Adicionales
10.1 Generación Automática
Para proyectos grandes, considerar usar scripts de Python con python-docx para generar archivos de prueba automáticamente.
10.2 Versionamiento
Los datos de prueba deben versionarse junto con el código en el repositorio:
word-editor-qa-portfolio/
└── test-data/
    └── documentos-prueba/
        └── [todos los archivos .docx]
10.3 Tamaño del Repositorio
Consideración: Los archivos Word pueden aumentar el tamaño del repositorio.
Alternativas:

Usar Git LFS para archivos grandes
Proporcionar script para generar archivos localmente