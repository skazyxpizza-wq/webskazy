# Lovable Orders Hub

Construí este sistema completo de una sola vez, con toda la lógica y

funcionamiento detallado a continuación.

NO simplifiques.

NO elimines funcionalidades.

NO reemplaces funcionalidades por versiones más simples.

NO comprimas ni resumas los requerimientos.

Todo debe implementarse de forma funcional y conectada de extremo a

extremo.

---

# 1. BASE DE DATOS

Usá Supabase como backend principal.

Estructurá y conectá correctamente las tablas necesarias para que todo

el sistema funcione de extremo a extremo:

- categorias

- productos

- pedidos

- pedido_items

- codigos_descuento

- cadetes

- accesos_sectores

- stock

- banners

- logos_categoria

- configuracion_general

La base de datos debe quedar preparada para que Cliente, Cocina,

Envíos y Admin trabajen sobre la misma información y se actualicen

en tiempo real.

---

# 2. REGLA GENERAL DE EDICIÓN

Absolutamente todo lo que sea contenido o configuración debe poder

editarse desde el panel de Administración sin modificar código.

Debe poder editarse:

- textos

- imágenes

- precios

- categorías

- orden de categorías

- productos

- disponibilidad de productos

- banners

- promociones

- tiempos de entrega

- contraseñas de otros sectores

- porcentajes de descuento

- cantidad de logos

- velocidad de la barra de logos

- duración de movimiento de la barra

- tutorial

- horarios del local

- configuración general

Todo cambio realizado desde Administración debe reflejarse

correctamente en las áreas correspondientes.

---

# 3. FLUJO GENERAL DEL SISTEMA

Cada pedido debe pasar por las siguientes etapas:

CLIENTE → COCINA → ENVÍOS → ENTREGADO

Las etapas deben estar sincronizadas en tiempo real mediante

Supabase Realtime.

Cuando un pedido cambie de estado, el cambio debe reflejarse

automáticamente en las áreas correspondientes.

---

# 4. PERSISTENCIA DE DATOS

Todo pedido confirmado debe guardarse en Supabase.

Guardar:

- código del pedido

- nombre del cliente

- teléfono

- domicilio

- productos comprados

- cantidades

- precio unitario

- subtotal

- descuento aplicado

- monto descontado

- monto total

- método de pago

- fecha

- hora

- estado

- información necesaria para la gestión del envío

Toda esta información debe poder visualizarse desde Administración.

Debe existir la posibilidad de descargar la información de pedidos

en formato Excel.

---

# 5. ZONA GEOGRÁFICA OBLIGATORIA PARA RECIBIR PEDIDOS

SKAZY SOLO debe aceptar pedidos cuya ubicación se encuentre DENTRO

del área geográfica delimitada por las siguientes coordenadas.

Las dos coordenadas representan ESQUINAS OPUESTAS de la zona permitida.

ESQUINA 1:

Latitud: -26.713999

Longitud: -65.271194

ESQUINA 2:

Latitud: -26.761972

Longitud: -65.233750

A partir de estas dos esquinas se debe formar un RECTÁNGULO

GEOGRÁFICO DE COBERTURA.

LÍMITES EXACTOS:

Latitud mínima:

-26.761972

Latitud máxima:

-26.713999

Longitud mínima:

-65.271194

Longitud máxima:

-65.233750

La ubicación solamente será válida cuando cumpla

simultáneamente:

latitud >= -26.761972

latitud <= -26.713999

longitud >= -65.271194

longitud <= -65.233750

## REGLA PRINCIPAL

Si las coordenadas de la ubicación del cliente están dentro de estos

cuatro límites:

→ PERMITIR EL PEDIDO.

Si las coordenadas están fuera de cualquiera de estos límites:

→ BLOQUEAR EL PEDIDO.

La restricción debe ser obligatoria y no debe existir ninguna forma

alternativa de saltarse esta validación.

Esta validación debe ejecutarse antes de permitir la confirmación

final del pedido.

## UBICACIÓN ACTUAL

Cuando el cliente presione:

"ENVIAR MI UBICACIÓN ACTUAL"

la aplicación debe solicitar la ubicación mediante la geolocalización

del navegador/dispositivo y obtener:

- latitud

- longitud

Después debe comprobar automáticamente si las coordenadas están

dentro del área permitida.

## UBICACIÓN MANUAL

Si el cliente selecciona una ubicación manualmente en el mapa,

también se deben obtener sus coordenadas y realizar exactamente

la misma validación.

Si la ubicación está fuera del área permitida, el pedido debe

quedar bloqueado.

## DIRECCIÓN

Cuando una dirección sea convertida a coordenadas, también debe

realizarse la validación geográfica.

No aceptar una dirección únicamente porque pertenezca a determinada

ciudad o localidad.

La decisión debe depender de las coordenadas geográficas reales.

## FUERA DE LA ZONA

Si la ubicación está fuera del área permitida, mostrar:

"Lo sentimos, por el momento no realizamos entregas en esta zona."

No permitir continuar con el pedido.

No permitir confirmar el pedido.

No permitir enviarlo por WhatsApp.

## DENTRO DE LA ZONA

Si la ubicación está dentro del área permitida, mostrar:

"Ubicación confirmada. Realizamos entregas en esta zona."

y permitir continuar normalmente.

## LÍMITES

Las coordenadas que se encuentren exactamente sobre cualquiera de

los límites también deben considerarse dentro de la zona permitida.

NO utilizar el nombre de la ciudad como criterio.

NO utilizar código postal.

NO utilizar barrio.

NO utilizar un radio circular.

NO ampliar automáticamente la zona.

NO aceptar ubicaciones cercanas que estén fuera de los límites.

La zona debe estar definida exclusivamente por las coordenadas

establecidas anteriormente.

Las coordenadas deben estar almacenadas en la configuración del

sistema para poder modificarlas posteriormente desde Administración

sin tener que modificar el código de toda la aplicación.

---

# 6. SECTOR 1 — CLIENTE

No requiere login.

No requiere contraseña.

No requiere creación de cuenta.

El cliente debe acceder directamente al menú.

Diseño mobile-first.

## MENÚ

- Mostrar el menú directamente al entrar.

- Botón de búsqueda mediante ícono que expande un campo de búsqueda.

- Botón de corazón en cada producto para marcar favoritos.

- Los favoritos deben funcionar como filtro general.

- Orden inicial de categorías:

  1. Promos

  2. Combos

  3. Pizzas

  4. Empanadas

  5. Resto

El orden debe poder modificarse desde Administración.

## PRODUCTOS

Cada producto debe permitir:

- nombre

- descripción

- precio

- imagen

- categoría

- visible/oculto

- agotado

- destacado/más vendido

Todos estos datos deben poder modificarse desde Administración.

---

# 7. PRESENTACIÓN DE PRODUCTOS

Los productos deben tener una presentación visual avanzada.

La imagen principal del producto debe mostrarse sin fondo.

Debe poder girar lentamente en sentido horario de forma continua.

Cuando el usuario pase el cursor sobre el producto o mantenga el dedo

sobre él en dispositivos táctiles:

- debe aparecer una segunda imagen

- la segunda imagen debe emerger desde la parte inferior del bloque

- no debe girar

- debe quedar quieta

- debe mostrarse poco más de la mitad

- al retirar el cursor o dedo, debe volver a bajar

Ambas imágenes deben poder reemplazarse desde Administración.

---

# 8. CARRITO

Al seleccionar un producto:

- agregarlo al carrito

- actualizar automáticamente la cantidad

- actualizar automáticamente el subtotal

- actualizar automáticamente el total

El carrito debe mostrar claramente los productos seleccionados.

---

# 9. CHECKOUT / RESUMEN

Reproducir esta estructura y textos:

"⚠️ Completá Nombre, Domicilio, Forma de pago y Tel/Celular antes de enviar."

Nombre:

[input]

Teléfono/Celular:

[input]

Escribí tu domicilio exacto o "Paso a Retirar":

[input]

"El vendedor determinará si llegamos a tu zona con el envío seleccionado."

## FORMA DE PAGO

💳 Forma de pago

💵 ¿Pagás con efectivo y necesitás vuelto?

Indicale al vendedor el monto con el que vas a pagar para que pueda

preparar el cambio.

Forma de pago:

[Seleccione forma de pago:

EFECTIVO / TRANSFERENCIA]

## TIEMPOS DE DEMORA

⏱ Tiempos de demora estimados

📅 Lun — Jue: 20 min – 40 min aprox.

📅 Vie — Dom: 35 min – 45 min aprox.

💬 ¿Dudas sobre el tiempo de entrega? Consultá con el vendedor

Los tiempos deben poder modificarse desde Administración.

## TOTAL

Mostrar:

Subtotal

Descuento

Total

Los productos deben aparecer apilados en filas.

El código de descuento debe aplicar el porcentaje configurado desde

Administración.

Ejemplo:

Subtotal: $20.000

Código: 40%

Mostrar:

"40%"

"-$8.000"

El subtotal y el total deben utilizar colores diferenciados.

Mostrar los importes dentro de un rectángulo con puntas redondeadas.

El total no debe verse exageradamente grande respecto al resto de la

interfaz.

---

# 10. ENVÍO DEL PEDIDO

El botón final debe:

1. Validar que todos los datos obligatorios estén completos.

2. Validar la zona geográfica.

3. Guardar el pedido en Supabase.

4. Crear el código único del pedido.

5. Establecer el estado inicial como "Cliente".

6. Preparar el mensaje completo.

7. Abrir WhatsApp al número del local.

El pedido debe enviarse mediante un único mensaje de WhatsApp.

No enviar mensajes separados por cada producto.

---

# 11. SUCURSALES

Mostrar:

"🚚 SUCURSALES SOLO CON ENVÍOS"

La configuración correspondiente debe poder administrarse desde

el panel de Administración.

---

# 13. SEGUIMIENTO DEL PEDIDO

No crear un sistema de registro tradicional para el cliente.

Los datos necesarios para identificar el pedido pueden conservarse

localmente en el dispositivo.

El cliente debe poder consultar:

- cantidad de pedidos

- qué pidió

- cuándo realizó el pedido

- estado actual del pedido

No mostrar el monto de pedidos anteriores en esta sección.

Mostrar el estado mediante etapas:

CLIENTE

↓

COCINA

↓

ENVÍOS

↓

ENTREGADO

Cada cambio de estado debe generar una notificación.

Al tocar la notificación, el cliente debe poder acceder al resumen

del pedido correspondiente.

Cuando el pedido se encuentre en:

ENVÍOS

el cliente podrá visualizar la ubicación del cadete.

Al completarse la entrega:

- dejar de mostrar la ubicación del cadete

- mostrar un panel indicando que la entrega está llegando/fue

  completada según corresponda

Pantalla final:

"cuenta con nosotros, siempre te atenderemos con el corazón en Skazy"

Mostrar el logo con corazón.

---

# 14. CANCELACIÓN

El cliente puede cancelar el pedido mientras se encuentre en:

CLIENTE

o

COCINA

Cuando se cancela:

- cambiar estado a cancelado

- quitarlo de las listas activas correspondientes

- registrar correctamente la cancelación

- enviar automáticamente el aviso de cancelación correspondiente

  por WhatsApp

No permitir cancelar un pedido que ya haya avanzado a ENVÍOS o

ENTREGADO.

---

# 15. TUTORIAL

Crear un tutorial para el primer acceso.

Debe mostrar paso a paso las principales funciones de la aplicación.

Utilizar:

- flechas

- formas

- indicadores visuales

- descripciones cortas

El usuario debe poder omitir pasos individuales.

No debe existir solamente un botón para cerrar todo el tutorial

sin permitir controlar los pasos.

El tutorial debe mostrarse una sola vez por cliente.

Debe poder activarse o desactivarse desde Administración.

---

# 16. ESTRUCTURA DE MARKETING

Dejar preparada la estructura de datos para:

- producto destacado

- producto más vendido

- fecha de expiración de banners

- promociones

- urgencia

- estado abierto/cerrado

- horarios configurables

También permitir configurar un texto de confianza en el checkout.

Ejemplo:

"Pago seguro · Entrega estimada · Sin costos ocultos"

---

# 17. SECTOR 2 — ADMINISTRACIÓN

Acceso:

/admin

Contraseña inicial:

Nereaaime8

No utilizar usuario.

La contraseña debe poder modificarse posteriormente.

## BARRA LATERAL

Crear las siguientes secciones independientes:

### 1. ACCESOS Y SEGURIDAD

Permitir administrar por separado:

- contraseña de Cocina

- contraseña de Envíos

Cada una debe tener su propio botón:

"Guardar"

---

### 2. CONTENIDO DEL MENÚ

CRUD completo de:

- categorías

- productos

Campos de productos:

- nombre

- descripción

- precio

- imagen

- orden

- categoría

- visible/oculto

- agotado

- destacado

- más vendido

Permitir agregar, editar, eliminar y reordenar.

---

### 3. CÓDIGOS DE DESCUENTO

CRUD completo.

Campos:

- nombre/código

- porcentaje

- activo/inactivo

- fecha de expiración opcional

---

### 4. BANNERS Y PROMOCIONES

CRUD completo de banners.

Permitir configurar:

- imagen

- título

- tamaño del título

- descripción

- tamaño de descripción

- tamaño del banner

- activo/inactivo

- destino al tocarlo

- orden

Los banners deben poder reordenarse.

---

### 5. BARRA DE LOGOS POR CATEGORÍA

Permitir configurar:

- cantidad de logos

- velocidad

- segundos de movimiento

- imagen

- título

---

### 6. PAGOS Y COBROS

Permitir configurar:

- imagen del QR

- alias: SKAZY.PZ

- Mercado Pago

- titular: Isaías Chaile

Mostrar vista previa del QR.

---

### 7. MAPA DE ENVÍOS EN VIVO

Mostrar las ubicaciones en tiempo real de los cadetes activos.

Esta sección es solamente de visualización para Administración.

---

### 8. BALANCES Y CADETES

Mostrar pedidos entregados.

Permitir filtros:

- día

- semana

- mes

Mostrar:

- total de efectivo

- total de transferencias

- información por cadete

---

### 9. HISTORIAL Y EXCEL

Crear tabla de pedidos con:

- código de pedido

- nombre

- teléfono

- detalle

- monto

- método de pago

- fecha

- hora

- estado

Los pedidos grupales deben combinarse correctamente mediante

un único código.

Permitir descargar los datos en Excel.

El Excel debe incluir:

- columnas ordenadas

- colores según estado

- totales automáticos

- sumas

- restas

- divisiones cuando correspondan

---

### 10. TUTORIAL DEL CLIENTE

Agregar un interruptor:

ACTIVO / INACTIVO

---

### 11. CONFIGURACIÓN GENERAL

Permitir configurar:

- horario del local

- textos del checkout

- tiempos de entrega

- mensajes

- configuración general

- coordenadas de la zona geográfica permitida

La zona geográfica debe poder modificarse desde Administración.

---

# 18. SECTOR 3 — COCINA

Acceso:

/cocina

Contraseña configurable desde Administración.

Diseño simple.

No utilizar animaciones innecesarias.

Utilizar letras grandes y fáciles de leer.

## FLUJO

Pedido del cliente

→ Cocina

→ Caja

Cada pedido debe aparecer en su propio bloque.

Los pedidos deben estar vinculados mediante:

- código

- número de pedido

- identificación visual

Cuando existan pedidos que deban agruparse en cajas:

mostrar los pedidos juntos y mantener siempre visible su código.

Ejemplo:

#0000

Al marcar un pedido como:

LISTO

debe pasar automáticamente a:

ENVÍOS

## STOCK

Crear un bloque de Stock.

Mostrar:

- ingredientes disponibles

- ingredientes faltantes

- avisos

El aviso de faltante debe poder configurarse.

## NOTIFICACIONES

Crear notificaciones mediante sonido.

Duración:

4 segundos.

Utilizarlas para las notificaciones correspondientes a las entregas

de cadetes.

Al tocar una notificación:

→ abrir el detalle del pedido.

---

# 19. SECTOR 4 — ENVÍOS

Acceso:

/envios

Contraseña configurable desde Administración.

Diseño simple.

No utilizar demasiados colores.

Cada pantalla debe tener arriba a la izquierda:

← Volver

## PEDIDOS

Crear bloque:

"Seleccionar paquetería en sucursal"

Debe estar activo solamente cuando Cocina esté activa.

El cadete debe poder:

- visualizar su ubicación

- visualizar la ubicación de la sucursal

- visualizar pedidos listos

- seleccionar pedidos

- deseleccionar pedidos

Los pedidos solamente deben retirarse de la selección mediante

cancelación o finalización correspondiente.

---

# 20. HOJA DE RUTA Y NAVEGACIÓN

Crear un sistema de navegación para cadetes.

Debe poder generar rutas considerando múltiples pedidos y múltiples

paradas.

La ruta debe priorizar recorridos eficientes.

Debe permitir reorganizar las paradas según corresponda.

La navegación debe funcionar en tiempo real.

Si el cadete se desvía:

→ recalcular la ruta

→ continuar guiándolo

Agregar asistencia por voz.

---

# 21. AL LLEGAR A CADA CLIENTE

Mostrar:

- resumen del pedido

- productos

- cantidades

- total

Diferenciar visualmente el total.

## TRANSFERENCIA

Mostrar:

- alias: SKAZY.PZ

- Mercado Pago

- titular: Isaías Chaile

- QR configurable desde Administración

todo pero absolutamente todo se puede modificar desde el pnale de admin. texto tittulos imagenes pequelos cosas vlocidad. 

## EFECTIVO

Mostrar:

- monto que debe pagar

- monto recibido

- vuelto

Mostrar el teléfono del cliente.

Permitir llamar al cliente.

Botón:

"Finalizar envío"

Al utilizarlo:

- marcar pedido como entregado

- guardar correctamente el balance

- actualizar Administración

- avanzar al siguiente pedido correspondiente

---

# 22. FINALIZACIÓN DE RUTA

Cuando el cadete haya completado todos los pedidos:

mostrar:

- notificación

- guía de regreso a la sucursal

Crear bloque:

"Rendición"

Mostrar:

- efectivo recaudado

- transferencias recibidas

- cantidad de pagos en efectivo

- cantidad de transferencias

- dinero físico que debe presentar

---

# 23. REGLAS GENERALES DE IMPLEMENTACIÓN

Todo debe funcionar de extremo a extremo.

Un pedido creado por el cliente debe:

1. Validar los datos obligatorios.

2. Validar la ubicación dentro de la zona permitida.

3. Guardarse en Supabase.

4. Recibir un código único.

5. Aparecer automáticamente en Cocina.

6. Poder pasar a Listo.

7. Aparecer automáticamente en Envíos.

8. Poder ser tomado por un cadete.

9. Mostrar el seguimiento correspondiente.

10. Poder finalizarse como Entregado.

11. Actualizar balances.

12. Aparecer correctamente en Administración.

13. Poder incluirse en la exportación a Excel.

Todas las áreas deben estar sincronizadas mediante Supabase Realtime.

No crear funcionalidades ficticias que solamente cambien visualmente

el estado.

Los cambios deben persistir realmente en la base de datos.

La aplicación debe manejar correctamente errores de conexión,

validaciones y estados de carga.

No permitir que un pedido pueda saltarse etapas.

No permitir que un pedido fuera de la zona geográfica establecida

pueda ser confirmado.

La aplicación debe quedar preparada para producción y todas las

funciones descritas deben estar realmente conectadas entre sí.

This project was built with [Lovable](https://lovable.dev).

**Live app**: https://skazy-connect.lovable.app

## Build with Lovable

Continue developing this project in the [Lovable editor](https://lovable.dev/projects/ee4e4b74-114d-4a30-9435-81f73161834a).

- **Ship faster**: describe what you want to build and Lovable handles the code.
- **Stay in sync**: every change made in Lovable is committed straight to this repository.
- **Full ownership**: this code is yours. Push to `main` on GitHub and your changes sync back into Lovable, ready for your next prompt.

## Development

Prefer working locally? You need Node.js and npm — [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating).

```sh
git clone <this-repository-url>
cd <repository-name>
npm i
npm run dev
```
