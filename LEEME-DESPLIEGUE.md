# SKAZY — Guía de despliegue y estado del proyecto

## 1. Qué incluye esta versión
- Tarjetas **Promo** (marco rojo, foto a la izquierda) y **Combo** (foto arriba, precio y botón negro) con estilos.
- **Pedido grupal** conectado al checkout (nombres, asignación de productos, pago por persona), al mensaje de WhatsApp y a la vista del cadete.
- **Cadetes:** sin "Cancelar selección"; flecha ← arriba a la izquierda; botón "Cómo llegar" (Google Maps con paradas y voz);
  validación de efectivo; rendición que respeta el pedido grupal; toma de pedido atómica (dos cadetes no pueden tomar el mismo).
- **Cocina:** interruptor "Cocina ACTIVA / en pausa". Hasta que Cocina la active, Envíos no muestra paquetería. (Por defecto: en pausa.)
- **Admin:** isologo centrado; subida de imágenes por archivo (producto, segunda imagen, QR, logos, anuncios) a Supabase Storage.
- El logo y el isologo ya **no dependen de Lovable**: se leen de `public/marca/`.
- Verificado: compila sin errores de tipos y `npm run build` finaliza correctamente.
  No se probó en un navegador ni contra la base de datos real.

## 2. Archivos que usted debe colocar
Copie sus archivos originales en `public/marca/` con estos nombres exactos:
- `logo-principal.png`
- `isologo.webp`
Mientras no existan, se muestra `public/marca/fallback.png` (provisorio, de baja calidad).

## 3. Base de datos (Supabase)
Hasta ahora la aplicación usaba una base administrada por Lovable Cloud (por eso nunca se le pidieron claves).
Para ser independiente, use su propio proyecto:
1. Cree un proyecto en supabase.com (plan gratuito). Guarde la contraseña de la base de datos.
2. Abra SQL Editor, pegue **todo** el contenido de `supabase/INSTALAR_TODO.sql` y presione Run.
   Crea las tablas, los datos de ejemplo, las funciones, el tiempo real, las columnas de personalización,
   el pedido grupal y el bucket de imágenes. (Probado desde cero en un PostgreSQL local: el esquema coincide con el que espera la aplicación.)
3. En Project Settings > API copie solo dos valores:
   - **Project URL**
   - **Clave pública** (anon / publishable)
   NUNCA use la clave secreta (service_role) en esta aplicación ni la suba a GitHub.
4. Cambie las contraseñas iniciales (Admin, Cocina y Envíos) desde el panel, en Accesos.
5. Los datos de prueba de Lovable Cloud no se transfieren; el menú se vuelve a cargar desde el Admin.

## 4. Publicación en Cloudflare (GitHub → Cloudflare)
1. Cree un repositorio **privado** en GitHub y suba el contenido de esta carpeta (sin `node_modules`).
2. Cloudflare > Workers & Pages > Create > importar repositorio de Git (Workers Builds).
3. Nombre del Worker: `skazy`.
4. Build command: `npm run build`   |   Deploy command: `npx wrangler deploy` (valor por defecto).
5. Build variables: `VITE_SUPABASE_URL`, `VITE_SUPABASE_PUBLISHABLE_KEY`, `SUPABASE_URL`, `SUPABASE_PUBLISHABLE_KEY`
   (valores de `.env.example`). Agregue también `SUPABASE_URL` y `SUPABASE_PUBLISHABLE_KEY` en Settings > Variables & Secrets (tiempo de ejecución).
6. Se publicará en una dirección `skazy.<su-cuenta>.workers.dev`.
   Este proyecto es de tipo servidor (Worker), no una página estática: no use "Pages > Vite > dist".

## 5. Pendiente (Etapa 2 — SEGURIDAD). No publique con clientes reales antes de completarla
- Hoy todas las tablas operativas permiten leer, modificar y borrar a cualquier visitante con la clave pública
  (datos de clientes, precios, pedidos). La contraseña de cada sector solo bloquea la pantalla, no los datos.
- Las contraseñas se guardan en texto plano y la inicial figura en la migración.
- Requiere: autenticación real por sector, políticas RLS restrictivas y funciones para crear/seguir/cancelar pedidos.
- La guía por calles dentro de la propia app requiere un servicio de rutas con clave de API; mientras tanto se usa "Cómo llegar" de Google Maps.
