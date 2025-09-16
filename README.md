


//Listar todos os clientes que não tenham realizado uma compra
SELECT c.ID_CLIENTE, c.FIRST_NAME, c.LAST_NAME
FROM CUSTOMERS c
LEFT JOIN ORDERS o
    ON c.ID_CLIENTE = o.CUSTOMER_ID
WHERE o.ORDER_ID IS NULL;


Explicação:

Usamos LEFT JOIN para trazer todos os clientes.

Se não houver pedido (ORDER_ID IS NULL), significa que o cliente não comprou.

2️⃣ Listar os produtos que não tenham sido comprados
SELECT p.PRODUCT_ID, p.PRODUCT_NAME
FROM PRODUCTS p
LEFT JOIN ORDER_ITEMS oi
    ON p.PRODUCT_ID = oi.PRODUCT_ID
WHERE oi.ORDER_ID IS NULL;


Explicação:

Mesma lógica do cliente: join entre produtos e itens de pedido.

Se não houver correspondência (ORDER_ID IS NULL), o produto nunca foi vendido.

3️⃣ Listar os produtos sem estoque
SELECT p.PRODUCT_ID, p.PRODUCT_NAME
FROM PRODUCTS p
LEFT JOIN STOCKS s
    ON p.PRODUCT_ID = s.PRODUCT_ID
WHERE s.QUANTITY IS NULL OR s.QUANTITY = 0;


Explicação:

Faz join entre produtos e estoque.

Se QUANTITY é zero ou nula, o produto está sem estoque.

4️⃣ Agrupar a quantidade de vendas de uma determinada marca por loja
SELECT st.STORE_NAME, b.BRAND_NAME, SUM(oi.QUANTITY) AS TOTAL_VENDAS
FROM ORDER_ITEMS oi
JOIN ORDERS o ON oi.ORDER_ID = o.ORDER_ID
JOIN PRODUCTS p ON oi.PRODUCT_ID = p.PRODUCT_ID
JOIN BRANDS b ON p.BRAND_ID = b.BRAND_ID
JOIN STORES st ON o.STORE_ID = st.STORE_ID
WHERE b.BRAND_NAME = 'NOME_DA_MARCA'
GROUP BY st.STORE_NAME, b.BRAND_NAME;


Explicação:

Faz join de todas as tabelas relevantes: pedidos → itens → produtos → marca → loja.

Filtra por marca específica e agrupa por loja.

5️⃣ Listar os funcionários que não estejam relacionados a um pedido
SELECT s.STAFF_ID, s.FIRST_NAME, s.LAST_NAME
FROM STAFF s
LEFT JOIN ORDERS o
    ON s.STAFF_ID = o.STAFF_ID
WHERE o.ORDER_ID IS NULL;


Explicação:

Mesma lógica de clientes não compraram.

Se não houver pedido associado ao funcionário (ORDER_ID IS NULL), ele não realizou pedidos.