# 🛒 Projeto Banco de Dados ECOMMERCE

## 📋 Descrição

Este projeto modela e implementa um banco de dados relacional para um sistema de **e-commerce**, com foco em gestão de clientes, produtos, pedidos, fornecedores, vendedores, entregas, departamentos e empregados.

Inclui criação de tabelas, índices para otimização, dados de exemplo (inserts) e uma procedure para manipulação dinâmica de dados na tabela `clients`.

---

## 🗂 Estrutura do Banco

- **clients**: informações dos clientes (pessoa física e jurídica).
- **product**: catálogo de produtos com categorias e classificações.
- **orders**: pedidos realizados pelos clientes.
- **productOrder**: relação entre produtos e pedidos.
- **productStorage** e **storageLocation**: gestão de estoque e localização.
- **supplier** e **productSupplier**: fornecedores e produtos fornecidos.
- **seller** e **productSeller**: vendedores e seus produtos.
- **payment_methods**: formas de pagamento associadas aos pedidos.
- **delivery**: status e informações de entrega.
- **departments** e **employees**: departamentos da empresa e seus empregados.

---

## ⚡ Índices Criados

| Índice                      | Coluna(s)            | Objetivo                                              |
|-----------------------------|----------------------|-------------------------------------------------------|
| idx_clients_cpf             | clients(cpf)         | Busca rápida por CPF de cliente (único e frequente).  |
| idx_product_category        | product(category)    | Consulta por categoria de produtos.                   |
| idx_orders_idOrderClient    | orders(idOrderClient)| Busca pedidos por cliente.                             |
| idx_productOrder_idPOorder  | productOrder(idPOorder)| Facilita joins e filtros entre pedidos e produtos.  |
| idx_productSupplier_idPsProduct | productSupplier(idPsProduct) | Busca produtos fornecidos.                     |
| idx_product_Pname           | product(Pname)       | Busca por nome de produto.                             |
| idx_delivery_status         | delivery(deliveryStatus) | Consulta por status de entrega.                      |
| idx_orders_status           | orders(orderStatus)  | Busca por status do pedido.                            |
| idx_department_city         | departments(city)    | Busca e agrupamento por cidade dos departamentos.     |
| idx_employee_department     | employees(idDepartment) | Busca empregados por departamento.                   |

---

## 🗃️ Dados de Exemplo (Inserts)

Foram inseridos dados de exemplo para as tabelas principais, facilitando testes e demonstrações.

---

## ⚙️ Procedure: `sp_manage_clients`

Procedure para operações dinâmicas (CRUD) na tabela `clients`, controlada por parâmetro de ação.

### Parâmetros

- `p_action INT`: ação a ser executada  
  - 1 = SELECT (busca todos ou por id)  
  - 2 = UPDATE  
  - 3 = DELETE  
  - 4 = INSERT  
- `p_idClient INT`: id do cliente (para SELECT por id, UPDATE, DELETE)  
- `p_Fname VARCHAR(10)`, `p_Minit CHAR(3)`, `p_Lname VARCHAR(20)`, `p_cpf CHAR(11)`, `p_address VARCHAR(255)`: dados do cliente

### Exemplos de chamada

```sql
-- 👁️ Selecionar todos os clientes
CALL sp_manage_clients(1, 0, NULL, NULL, NULL, NULL, NULL);

-- ✏️ Atualizar cliente com id 2
CALL sp_manage_clients(2, 2, 'NovoNome', 'N', 'Sobrenome', '00012345678', 'Novo endereço');

-- 🗑️ Deletar cliente com id 3
CALL sp_manage_clients(3, 3, NULL, NULL, NULL, NULL, NULL);

-- ➕ Inserir novo cliente
CALL sp_manage_clients(4, NULL, 'Lucas', 'L', 'Silva', '12345678900', 'Rua Nova 123');
````
---

### 🚀 Como Usar
1. Execute o script de criação do banco ECOMMERCE e das tabelas.

2. Execute o script para criação dos índices.

3. Insira os dados de exemplo.

4. Crie a procedure sp_manage_clients.

5. Utilize os comandos CALL para manipular dados na tabela clients.

---

### ⚠️ Observações
- A procedure está criada apenas para clients, mas pode ser adaptada para outras tabelas.

- Índices foram criados para otimizar consultas frequentes.

- Integridade referencial garantida via constraints e chaves estrangeiras.

- Atualizações e deleções devem ser feitas com cautela para evitar perda de dados.

