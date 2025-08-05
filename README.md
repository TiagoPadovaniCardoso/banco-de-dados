# Explorando Banco de Dados Relacional, Não Relacional e Normalização

## 1. Conceitos Teóricos

### Banco de Dados Relacional
Um banco de dados relacional armazena dados em tabelas com colunas (atributos) e linhas (registros). As tabelas são relacionadas entre si por chaves primárias e estrangeiras.

Exemplo de uso: Um sistema escolar, com tabelas para alunos, cursos e matrículas.

### Banco de Dados Não Relacional
Bancos de dados não relacionais (NoSQL) não utilizam tabelas. Eles armazenam dados em formatos flexíveis, como documentos JSON, grafos ou pares chave-valor.

Exemplo de uso: Um aplicativo de redes sociais que salva postagens com comentários embutidos no mesmo documento.

### Normalização
Normalização é o processo de organizar os dados em tabelas para reduzir redundâncias e garantir a integridade dos dados.

Objetivo: Dividir tabelas grandes em menores, com dados bem organizados e relacionados, evitando repetições e facilitando atualizações.

## 2. Tabela Não Normalizada

| Pedido_ID | Cliente_Nome | Cliente_Endereco | Produto_ID | Produto_Nome | Quantidade | Preco_Total |
|-----------|---------------|------------------|-------------|----------------|------------|--------------|
| 1         | João Silva    | Rua A, 123       | 10          | Caneta         | 2          | 4,00         |
| 1         | João Silva    | Rua A, 123       | 11          | Lápis          | 1          | 2,00         |
| 2         | Maria Souza   | Av. B, 456       | 10          | Caneta         | 5          | 10,00        |

## 3. Normalização até a 3ª Forma Normal (3FN)

### 1ª Forma Normal (1FN)
- Eliminamos grupos repetidos.
- Cada campo contém apenas um valor.
- A tabela anterior já foi convertida para esse formato.

### 2ª Forma Normal (2FN)
- Removemos dependências parciais.
- Criamos tabelas separadas para Clientes e Produtos.

### 3ª Forma Normal (3FN)
- Removemos dependências transitivas.
- Criamos as seguintes tabelas:

**Clientes**

| Cliente_ID | Nome        | Endereco     |
|------------|-------------|--------------|
| 1          | João Silva  | Rua A, 123   |
| 2          | Maria Souza | Av. B, 456   |

**Produtos**

| Produto_ID | Nome   |
|------------|--------|
| 10         | Caneta |
| 11         | Lápis  |

**Pedidos**

| Pedido_ID | Cliente_ID |
|-----------|------------|
| 1         | 1          |
| 2         | 2          |

**Itens_Pedido**

| Pedido_ID | Produto_ID | Quantidade | Preco_Total |
|-----------|-------------|------------|--------------|
| 1         | 10          | 2          | 4,00         |
| 1         | 11          | 1          | 2,00         |
| 2         | 10          | 5          | 10,00        |

### Relacionamentos
- A tabela Pedidos se relaciona com a tabela Clientes via Cliente_ID.
- A tabela Itens_Pedido conecta Pedidos e Produtos por Pedido_ID e Produto_ID.

## 4. Modelo Não Relacional (MongoDB)

```json
{
  "pedido_id": 1,
  "cliente": {
    "nome": "João Silva",
    "endereco": "Rua A, 123"
  },
  "itens": [
    {
      "produto_id": 10,
      "nome": "Caneta",
      "quantidade": 2,
      "preco_total": 4.00
    },
    {
      "produto_id": 11,
      "nome": "Lápis",
      "quantidade": 1,
      "preco_total": 2.00
    }
  ]
}
