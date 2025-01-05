Aqui está uma lista com **20 exercícios SQL** que abrangem vários conceitos, do básico ao avançado. No final, você encontrará o gabarito com as respostas.

---

### **Lista de Exercícios SQL**

#### **Fáceis**
1. Liste todos os dados da tabela `Clientes`.
2. Exiba apenas os nomes e emails dos clientes.
3. Liste os produtos cujo preço seja maior que 100.
4. Liste todos os clientes ordenados por nome em ordem alfabética.
5. Conte quantos produtos estão disponíveis no estoque.

#### **Intermediários**
6. Liste os clientes que vivem no estado "SP" ou "RJ".
7. Mostre o nome e o preço dos produtos que têm estoque maior que 50.
8. Calcule o total de estoque disponível na tabela `Produtos`.
9. Liste os clientes que foram cadastrados após "2023-01-01".
10. Liste os pedidos cujo total seja maior que 1000.

#### **`JOINs` Simples**
11. Mostre os nomes dos clientes e os IDs de seus pedidos.
12. Liste os produtos comprados em cada pedido com seus respectivos preços.
13. Mostre o nome dos clientes que compraram o produto "Cadeira Gamer".
14. Liste todos os pedidos, incluindo clientes que ainda não fizeram pedidos (use `LEFT JOIN`).
15. Liste os produtos que nunca foram vendidos (use `LEFT JOIN` e filtre nulos).

#### **Subconsultas e Agregações**
16. Encontre o produto mais caro na tabela `Produtos`.
17. Liste os clientes que fizeram mais de 2 pedidos.
18. Mostre o nome do cliente que gastou o maior valor total em pedidos.
19. Liste os produtos cujo preço esteja acima da média de preços da tabela.
20. Exiba o pedido que contém o maior número de itens.

---

### **Gabarito**

#### **Fáceis**
1. ```sql
   SELECT * FROM Clientes;
   ```

2. ```sql
   SELECT Nome, Email FROM Clientes;
   ```

3. ```sql
   SELECT * FROM Produtos WHERE Preco > 100;
   ```

4. ```sql
   SELECT * FROM Clientes ORDER BY Nome ASC;
   ```

5. ```sql
   SELECT COUNT(*) AS TotalProdutos FROM Produtos;
   ```

#### **Intermediários**
6. ```sql
   SELECT * FROM Clientes WHERE Estado IN ('SP', 'RJ');
   ```

7. ```sql
   SELECT NomeProduto, Preco FROM Produtos WHERE Estoque > 50;
   ```

8. ```sql
   SELECT SUM(Estoque) AS TotalEstoque FROM Produtos;
   ```

9. ```sql
   SELECT * FROM Clientes WHERE DataCadastro > '2023-01-01';
   ```

10. ```sql
    SELECT * FROM Pedidos WHERE TotalPedido > 1000;
    ```

#### **`JOINs` Simples**
11. ```sql
    SELECT c.Nome, p.PedidoID FROM Clientes c
    INNER JOIN Pedidos p ON c.ClienteID = p.ClienteID;
    ```

12. ```sql
    SELECT p.PedidoID, pr.NomeProduto, i.PrecoUnitario
    FROM Pedidos p
    INNER JOIN ItensPedidos i ON p.PedidoID = i.PedidoID
    INNER JOIN Produtos pr ON i.ProdutoID = pr.ProdutoID;
    ```

13. ```sql
    SELECT c.Nome FROM Clientes c
    INNER JOIN Pedidos p ON c.ClienteID = p.ClienteID
    INNER JOIN ItensPedidos i ON p.PedidoID = i.PedidoID
    INNER JOIN Produtos pr ON i.ProdutoID = pr.ProdutoID
    WHERE pr.NomeProduto = 'Cadeira Gamer';
    ```

14. ```sql
    SELECT c.Nome, p.PedidoID FROM Clientes c
    LEFT JOIN Pedidos p ON c.ClienteID = p.ClienteID;
    ```

15. ```sql
    SELECT NomeProduto FROM Produtos p
    LEFT JOIN ItensPedidos i ON p.ProdutoID = i.ProdutoID
    WHERE i.ProdutoID IS NULL;
    ```

#### **Subconsultas e Agregações**
16. ```sql
    SELECT NomeProduto, Preco FROM Produtos
    WHERE Preco = (SELECT MAX(Preco) FROM Produtos);
    ```

17. ```sql
    SELECT c.Nome FROM Clientes c
    INNER JOIN Pedidos p ON c.ClienteID = p.ClienteID
    GROUP BY c.Nome
    HAVING COUNT(p.PedidoID) > 2;
    ```

18. ```sql
    SELECT c.Nome FROM Clientes c
    INNER JOIN Pedidos p ON c.ClienteID = p.ClienteID
    GROUP BY c.Nome
    ORDER BY SUM(p.TotalPedido) DESC
    LIMIT 1;
    ```

19. ```sql
    SELECT NomeProduto FROM Produtos
    WHERE Preco > (SELECT AVG(Preco) FROM Produtos);
    ```

20. ```sql
    SELECT i.PedidoID, COUNT(i.ItemID) AS TotalItens
    FROM ItensPedidos i
    GROUP BY i.PedidoID
    ORDER BY TotalItens DESC
    LIMIT 1;
    ```

---

Esses exercícios devem ajudar a consolidar seus conhecimentos de SQL. Se quiser personalizar ou ajustar algo, é só avisar!
