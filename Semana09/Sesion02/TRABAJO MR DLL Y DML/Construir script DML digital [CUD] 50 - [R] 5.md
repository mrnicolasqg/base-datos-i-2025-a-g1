-- === INSERTS ===
INSERT INTO persona VALUES (1, 'Ana', 'García', '1992-05-10', 'ana.garcia@mail.com', 'Calle 10 #5-20', '3000000001');
INSERT INTO persona VALUES (2, 'Jorge', 'Ramírez', '1988-09-22', 'jorge.ramirez@mail.com', 'Calle 11 #6-21', '3000000002');
INSERT INTO persona VALUES (3, 'Lucía', 'Pérez', '1995-02-18', 'lucia.perez@mail.com', 'Calle 12 #7-22', '3000000003');
INSERT INTO persona VALUES (4, 'Luis', 'Mendoza', '1980-03-30', 'luis.mendoza@mail.com', 'Calle 13 #8-23', '3000000004');
INSERT INTO persona VALUES (5, 'Elena', 'Díaz', '1999-12-25', 'elena.diaz@mail.com', 'Calle 14 #9-24', '3000000005');

INSERT INTO cliente VALUES (1, 'C001', '2024-01-01', 1);
INSERT INTO cliente VALUES (2, 'C002', '2024-02-01', 2);

INSERT INTO empleado VALUES (1, 'E001', '2023-01-01', 2500000, 'Indefinido', 3);
INSERT INTO empleado VALUES (2, 'E002', '2022-05-10', 3200000, 'Fijo', 4);

INSERT INTO categoria VALUES (1, 'Electrónica', 'Dispositivos y accesorios');
INSERT INTO categoria VALUES (2, 'Hogar', 'Productos para el hogar');
INSERT INTO categoria VALUES (3, 'Juguetería', 'Juguetes para niños');

INSERT INTO metodo_pago VALUES (1, 'Tarjeta de Crédito', 'Pago con tarjeta');
INSERT INTO metodo_pago VALUES (2, 'Efectivo', 'Pago en efectivo');
INSERT INTO metodo_pago VALUES (3, 'Transferencia', 'Pago bancario');

INSERT INTO producto VALUES (1, 'P001', 'Televisor LG', 'Smart TV 55 pulgadas', 1);
INSERT INTO producto VALUES (2, 'P002', 'Aspiradora', 'Aspiradora sin cable', 2);
INSERT INTO producto VALUES (3, 'P003', 'Muñeca Barbie', 'Edición especial', 3);

INSERT INTO inventario VALUES (1, 'Lote Enero', '2025-01-05', 2100000, 10, '2025-01-01', '2026-01-01', 1);
INSERT INTO inventario VALUES (2, 'Lote Febrero', '2025-02-05', 550000, 30, '2025-02-01', '2026-02-01', 2);
INSERT INTO inventario VALUES (3, 'Lote Marzo', '2025-03-10', 120000, 100, '2025-03-01', '2026-03-01', 3);

INSERT INTO factura VALUES (1, 'F001', '2025-04-01', 2100000, 0, 0, 2100000, 1, 1);
INSERT INTO factura VALUES (2, 'F002', '2025-04-02', 600000, 50000, 0, 550000, 2, 2);

INSERT INTO detalle_factura VALUES (1, 1, 0, 0, 2100000, 1, 1);
INSERT INTO detalle_factura VALUES (2, 1, 10, 0, 550000, 2, 2);

-- === UPDATES ===
UPDATE persona SET telefono = '3111111111' WHERE id = 1;
UPDATE persona SET direccion = 'Av 9 #23-45' WHERE id = 2;
UPDATE cliente SET fecha_vinculacion = '2024-03-01' WHERE id = 1;
UPDATE empleado SET salario = 2700000 WHERE id = 1;
UPDATE producto SET nombre = 'Smart TV LG 55"' WHERE id = 1;
UPDATE inventario SET stock = 8 WHERE id = 1;
UPDATE factura SET valor_descuento = 100000 WHERE id = 2;
UPDATE detalle_factura SET porcentaje_descuento = 15 WHERE id = 2;
UPDATE categoria SET descripcion = 'Tecnología y accesorios' WHERE id = 1;
UPDATE metodo_pago SET nombre = 'Tarjeta Débito' WHERE id = 1;

-- === DELETES (condicionales, para evitar errores si hay relaciones) ===
DELETE FROM detalle_factura WHERE id = 2;
DELETE FROM detalle_factura WHERE id = 1;
DELETE FROM factura WHERE id = 2;
DELETE FROM factura WHERE id = 1;
DELETE FROM inventario WHERE id = 3;
DELETE FROM inventario WHERE id = 2;
DELETE FROM inventario WHERE id = 1;
DELETE FROM producto WHERE id = 3;
DELETE FROM producto WHERE id = 2;
DELETE FROM producto WHERE id = 1;
DELETE FROM categoria WHERE id = 3;
DELETE FROM categoria WHERE id = 2;
DELETE FROM categoria WHERE id = 1;
DELETE FROM metodo_pago WHERE id = 3;
DELETE FROM metodo_pago WHERE id = 2;
DELETE FROM metodo_pago WHERE id = 1;
DELETE FROM cliente WHERE id = 2;
DELETE FROM cliente WHERE id = 1;
DELETE FROM empleado WHERE id = 2;
DELETE FROM empleado WHERE id = 1;
DELETE FROM persona WHERE id = 5;
DELETE FROM persona WHERE id = 4;
DELETE FROM persona WHERE id = 3;
DELETE FROM persona WHERE id = 2;
DELETE FROM persona WHERE id = 1;

-- 1. Listar todos los productos con su categoría
SELECT p.nombre AS producto, c.nombre AS categoria
FROM producto p
JOIN categoria c ON p.categoria_id = c.id;

-- 2. Mostrar clientes con su nombre completo y fecha de vinculación
SELECT cl.codigo, per.nombre || ' ' || per.apellido AS cliente, cl.fecha_vinculacion
FROM cliente cl
JOIN persona per ON cl.persona_id = per.id;

-- 3. Inventario de productos con stock mayor a 20
SELECT i.nombre AS lote, p.nombre AS producto, i.stock
FROM inventario i
JOIN producto p ON i.producto_id = p.id
WHERE i.stock > 20;

-- 4. Facturas con valor bruto y neto
SELECT codigo, valor_bruto, valor_neto
FROM factura;

-- 5. Empleados con salario mayor a 2.5 millones
SELECT e.codigo, p.nombre || ' ' || p.apellido AS empleado, e.salario
FROM empleado e
JOIN persona p ON e.persona_id = p.id
WHERE e.salario > 2500000;
