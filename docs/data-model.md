# Modelagem de Dados

## Entidades

### Pedido (orders)
| Coluna | Tipo | Descrição |
| :--- | :--- | :--- |
| `id` | String (UUID) | Identificador único do pedido gerado automaticamente (Chave Primária). |
| `customer` | String | Identificação do cliente que realizou o pedido. |
| `status` | String | Status atual do pedido (padrão: "open"). |
| `created_at` | DateTime | Data e hora exata da criação do pedido (UTC). |

### Item (items)
| Coluna | Tipo | Descrição |
| :--- | :--- | :--- |
| `id` | String (UUID) | Identificador único do item gerado automaticamente (Chave Primária). |
| `order_id` | String | Referência ao pedido correspondente (Chave Estrangeira). |
| `sku` | String | Código identificador (Stock Keeping Unit) do produto. |
| `description` | String | Descrição do produto. |
| `quantity` | Integer | Quantidade do item no pedido. |

## Relacionamento
O modelo de dados estabelece um relacionamento **1:N (Um para Muitos)** entre Pedidos e Itens. 
Isso significa que um único Pedido (`orders`) pode conter múltiplos Itens (`items`), mas cada Item pertence exclusivamente a um único Pedido. 

A integridade desse relacionamento é garantida pela coluna `order_id` na tabela de itens, que atua como chave estrangeira. Há também uma regra de exclusão em cascata configurada (`cascade="all, delete-orphan"`), garantindo que, se um pedido for excluído do banco, todos os itens vinculados a ele também serão removidos automaticamente.

## Como as tabelas são criadas
A criação das tabelas no banco de dados não exige a execução manual de scripts SQL. A aplicação utiliza o **SQLAlchemy**, uma biblioteca de ORM (Object-Relational Mapping), para mapear as classes Python em tabelas do banco de dados relacional. 

Durante a inicialização da aplicação, as tabelas são criadas automaticamente no PostgreSQL (caso não existam) utilizando o mecanismo de migração embutido (`create_all()`).
