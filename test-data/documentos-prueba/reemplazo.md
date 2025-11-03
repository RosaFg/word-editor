2.3 Archivos para Pruebas de Reemplazo
2.3.1 reemplazo-selectivo.docx
Propósito: Probar reemplazo selectivo con múltiples coincidencias
Contenido:
El cliente visitó la tienda.
El cliente compró productos.
El cliente está satisfecho.
El precio es para el cliente.
Coincidencias: "cliente" aparece 4 veces
Uso: TC-004 (Reemplazo selectivo)
Escenario de prueba:

Buscar: "cliente"
Reemplazar por: "comprador"
Aceptar: 1ra y 3ra coincidencia
Rechazar: 2da y 4ta coincidencia

Resultado esperado:
El comprador visitó la tienda.
El cliente compró productos.
El comprador está satisfecho.
El precio es para el cliente.

2.3.2 reemplazo-masivo-multi.docx (Set de 2 archivos)
Propósito: Probar reemplazo masivo en múltiples documentos
archivo1.docx:
El precio actual es $100.
El precio incluye IVA.
Consulta el precio final.
archivo2.docx:
El precio de lista es estándar.
Revisa el precio en la web.
Total coincidencias: "precio" aparece 5 veces (3 en archivo1, 2 en archivo2)
Uso: TC-005 (Reemplazo masivo)
Escenario:

Buscar: "precio"
Reemplazar por: "costo"
Resultado: Todas las 5 coincidencias deben reemplazarse