# Práctica 3 — Tajinaste S.A.

## Contenido
- `modelo_er.drawio` y `modelo_er.png`: modelo conceptual de la práctica 2.
- `modelo_relacional.drawio` y `modelo_relacional.png`: transformación a tablas (PK/FK).
- `viveros.sql`: creación de la base de datos, tablas, restricciones, datos de prueba, ejemplos de DELETE y SELECT.

## Ejecución
```bash
psql -U postgres -d postgres -f viveros.sql
```
En Ubuntu, si se usa autenticación local peer:
```bash
sudo -u postgres psql -d postgres -f /ruta/absoluta/viveros.sql
```
El script usa comandos propios de `psql` (`\gexec` y `\connect`), por lo que debe ejecutarse con `psql`, no pegándolo directamente en un editor SQL genérico.

## Modelo
Las relaciones N:M STOCK, DESTINO y DESEMPEÑA se representan como tablas. Las relaciones 1:N TIENE, GESTIONA y REALIZA se representan con claves foráneas. Se añaden identificadores técnicos a DESTINO y DESEMPEÑA para permitir historiales repetidos.

## Decisiones
- `bonificacion` se interpreta como porcentaje (0–100).
- `productividad` se almacena como valor opcional no negativo porque no se proporciona fórmula de cálculo.
- `importe_total` se almacena como importe no negativo porque el modelo original no contiene líneas de pedido ni precios para calcularlo. Si se exige que sea derivado, habría que ampliar el modelo.
- `fecha_ingreso_plus` puede ser NULL para clientes no adheridos.
- Se impide eliminar productos, empleados y clientes con ciertas referencias activas; al eliminar una zona se eliminan sus relaciones de stock y destino.
- El modelo de la práctica 2 no contiene mantenimiento. Si la modificación posterior sobre tareas de mantenimiento forma parte del enunciado definitivo, se debe añadir una tabla MANTENIMIENTO y actualizar ambos diagramas.

## Comprobación
El script termina con SELECT de las diez tablas. Guardar capturas de sus resultados en `capturas/`. Las operaciones DELETE de ejemplo se ejecutan dentro de una transacción revertida con ROLLBACK, de modo que no se pierde el mínimo de cinco filas por tabla.

## Entrega
Subir todos los archivos al repositorio de GitHub y entregar el enlace. Si el repositorio es privado, invitar a cexposit@ull.edu.es.
