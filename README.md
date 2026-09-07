# travelers

Sitio de referencia del proyecto **flight-hunter**, publicado con GitHub Pages
en <https://maujpok.github.io/travelers/>.

## Para qué existe este repo

Para tener una URL propia que registrar como sitio web en los programas de
afiliados de viajes, **sin tocar el dominio del producto**.

Travelpayouts —el proveedor de precios de grilla de flight-hunter— no entrega
el token de su Data API hasta verificar que su script de monetización
("Drive") se sirve desde el sitio registrado en la cuenta. No hay forma de
saltear ese paso: mientras el asistente esté pendiente, su panel intercepta
todas las rutas, incluidas las que su documentación da para el token.

Ese script **no puede vivir en flight-hunter**. La página de privacidad del
producto, que ya está publicada, promete que no hay scripts de terceros ni
cookies de seguimiento — y el snippet de Drive trae `data-cmp-ab="2"`, o sea
que está hecho para poner un cartel de consentimiento. Además, la suite de
tests del producto mide Core Web Vitals en la primera carga, y un script de
terceros en la home es lo que la pone en rojo.

Así que el tag va acá.

## Cómo se usa

1. En el asistente de Travelpayouts, pantalla **«Install Drive manually»**,
   copiar el snippet.
2. Pegarlo en el `<head>` de [`index.html`](index.html), donde está el
   comentario que lo indica.
3. Commit y push. GitHub Pages redespliega en ~1 minuto.
4. Comprobar que quedó sirviéndose:

   ```bash
   curl -sS https://maujpok.github.io/travelers/ | grep -c emrldtp   # > 0
   ```

5. Volver al asistente y apretar **«Check Drive connection»**.

El tag conviene dejarlo puesto: una re-verificación del proveedor no vuelve a
frenar nada.

## Ojo con el orden

El verificador busca el script en el **sitio registrado en la cuenta**, y esa
URL puede quedar bloqueada. En el primer intento quedó registrado el dominio
de producción de flight-hunter y la cuenta ya no permitió cambiarlo, lo que
dejaba como única salida servir el tag en el producto. De ahí este repo.

Al crear una cuenta de afiliado, registrar **esta** URL, no la del producto.
