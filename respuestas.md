# Repuestas
---

## Pregunta 1 — Catálogo comercial activo

**Enunciado:** El equipo de ventas prepara la tarifa de la próxima campaña y necesita el catálogo depurado.
Obtén los productos que **no** están descatalogados y cuyo precio unitario esté entre 10 y 50 euros, ambos incluidos. Muestra el nombre del producto y su precio redondeado a dos decimales, ordenado de mayor a menor precio.

**Consulta:**

```sql
SELECT
	PRODUCT_NAME AS PRODUCTO,
	ROUND(UNIT_PRICE::NUMERIC, 2) AS PRECIO
FROM
	PRODUCTS
WHERE
	UNIT_PRICE BETWEEN 10 AND 50
	AND DISCONTINUED = 0
ORDER BY
	UNIT_PRICE DESC;
```

**Resultado:**

![Resultado Pregunta 1](images/respuesta01.png)

**Comentario:** Utilizo los alias en ambos campos del select para poder visualizarlo en español. Utilizo ::numeric en unit_price dentro del round() para evitar errores con el tipo de dato real e indico el número 2 ya que es la cantidad de decimales que quiero. En el where he usado between para poder filtrar con un rango y luego comparo discontinued = 0 porque 0 es que el producto está continuado y 1 es que está descontinuado.

---

## Pregunta 2 — Concentración geográfica de la cartera

**Enunciado:** Dirección quiere saber en qué mercados está realmente concentrada la base de clientes antes de decidir dónde abrir delegación.
Cuenta cuántos clientes hay en cada país y muestra únicamente aquellos países con **5 o más clientes**, ordenados de mayor a menor. Indica también cuántas ciudades distintas hay en cada uno de esos países.

**Consulta:**

```sql
SELECT
	COUNTRY AS PAIS,
	COUNT(CUSTOMER_ID) AS NUM_CLIENTES,
	COUNT(DISTINCT CITY) AS NUM_CIUDADES
FROM
	CUSTOMERS
GROUP BY
	COUNTRY
HAVING
	COUNT(CUSTOMER_ID) >= 5
ORDER BY
	COUNT(CUSTOMER_ID) DESC;
```

**Resultado:**

![Resultado Pregunta 2](images/respuesta02.png)

**Comentario:** ...

## Pregunta 3 — Alerta de reposición

**Enunciado:** Logística necesita detectar qué referencias están en riesgo de rotura de stock.
Localiza los productos activos cuyas unidades en stock sean **inferiores o iguales** a su nivel de reposición. Muestra el nombre, las unidades en stock, el nivel de reposición, las unidades ya pedidas al proveedor y una columna de texto que indique `'CRÍTICO'` cuando el stock sea 0 y `'AVISO'` en el resto de casos.

**Consulta:**

```sql
SELECT
	PRODUCT_NAME AS PRODCUTO,
	UNITS_IN_STOCK AS STOCK,
	REORDER_LEVEL AS NIVEL_REPOSICION,
	UNITS_ON_ORDER AS PEDIDO_A_PROVEEDOR,
	CASE
		WHEN UNITS_IN_STOCK = 0 THEN 'CRÍTICO'
		ELSE 'AVISO'
	END AS SITUACION
FROM
	PRODUCTS
WHERE
	UNITS_IN_STOCK <= REORDER_LEVEL;
```

**Resultado:**

![Resultado Pregunta 3](images/respuesta03.png)

**Comentario:** ...