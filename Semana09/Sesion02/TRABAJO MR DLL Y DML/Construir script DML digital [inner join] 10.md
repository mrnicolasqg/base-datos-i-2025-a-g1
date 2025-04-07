-- 1. Productos con su categoría
SELECT p.nombre AS producto, c.nombre AS categoria
FROM producto p
INNER JOIN categoria c ON p.categoria_id = c.id;

-- 2. Clientes con nombre completo y su correo
SELECT cl.codigo AS codigo_cliente, pe.nombre || ' ' || pe.apellido AS nombre_completo, pe.correo
FROM cliente cl
INNER JOIN persona pe ON cl.persona_id = pe.id;

-- 3. Empleados con nombre, tipo de contrato y salario
SELECT e.codigo, pe.nombre, pe.apellido, e.tipo_contrato, e.salario
FROM empleado e
INNER JOIN persona pe ON e.persona_id = pe.id;

-- 4. Inventario con nombre de producto
SELECT i.nombre AS lote, i.stock, p.nombre AS producto
FROM inventario i
INNER JOIN producto p ON i.producto_id = p.id;

-- 5. Facturas con nombre del cliente
SELECT f.codigo AS factura, per.nombre || ' ' || per.apellido AS cliente, f.valor_neto
FROM factura f
INNER JOIN cliente cl ON f.cliente_id = cl.id
INNER JOIN persona per ON cl.persona_id = per.id;

-- 6. Detalle de factura con nombre del producto
SELECT df.id, p.nombre AS producto, df.cantidad, df.subtotal
FROM detalle_factura df
INNER JOIN producto p ON df.producto_id = p.id;

-- 7. Facturas con método de pago
SELECT f.codigo AS factura, mp.nombre AS metodo_pago
FROM factura f
INNER JOIN metodo_pago mp ON f.medio_pago_id = mp.id;

-- 8. Detalles de factura con factura y producto
SELECT f.codigo AS factura, p.nombre AS producto, df.cantidad
FROM detalle_factura df
INNER JOIN factura f ON df.factura_id = f.id
INNER JOIN producto p ON df.producto_id = p.id;

-- 9. Empleado con fecha de vinculación y correo
SELECT e.codigo, pe.nombre, e.fecha_vinculacion, pe.correo
FROM empleado e
INNER JOIN persona pe ON e.persona_id = pe.id;

-- 10. Clientes y sus facturas
SELECT p.nombre || ' ' || p.apellido AS cliente, f.codigo AS factura, f.valor_neto
FROM factura f
INNER JOIN cliente c ON f.cliente_id = c.id
INNER JOIN persona p ON c.persona_id = p.id;
