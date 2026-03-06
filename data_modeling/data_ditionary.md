Este documento, contém de forma especificada e detalhada as regras de integridade ou restrições (constraints)
que serão implementadas para cada um dos dados das entidades dentro do sistema, no contexto de "SQL".

# Dicionário de dados

---

## 1.0. Tabela `Leitor`

Esta tabela armazena as credenciais e o perfil dos utilizadores.

| Campo | Tipo SQL       | Restrições (Constraints)         | Descrição / Regra de Negócio |
| --- |----------------|----------------------------------| --- |
| `id` | `BIGINT`       | **PK**, Not Null, auto_increment | Identificador único do registo. |
| `p_nome` | `VARCHAR(50)`  | Not Null                         | Primeiro nome do leitor. |
| `sb_nome` | `VARCHAR(100)` | Not Null                         | Sobrenome do leitor. |
| `email` | `VARCHAR(150)` | **Unique**, Not Null             | Deve ser um e-mail válido e único no sistema. |
| `genero` | `VARCHAR(20)`  | Not Null                         | Mapeado para um **Enum** (MASCULINO, FEMININO). |
| `palavra_passe` | `VARCHAR(255)` | Not Null                         | Armazenada obrigatoriamente com Hash (**BCrypt**). |
| `data_nasc` | `DATE`         | Not Null                         | Deve garantir que o leitor tenha uma idade válida. |

---

### 2.0. Dicionário de Dados: Tabela `Pagamento`

Esta é a tabela mais sensível do sistema, pois controla o acesso ao conteúdo pago.

| Campo | Tipo SQL       | Restrições (Constraints) | Descrição / Regra de Negócio |
| --- |----------------| --- | --- |
| `id` | `BIGINT`       | **PK**, Not Null | Identificador único do registo. |
| `metodo` | `VARCHAR(30)`  | Not Null | **Enum** (MCX_EXPRESS, TRANSFERENCIA, UNITEL_MONEY). |
| `estado` | `VARCHAR(20)`  | Not Null | **Enum** (PENDENTE, ANALISE, APROVADO, REJEITADO). |
| `url_comprov` | `VARCHAR(500)` | Nullable | Link para o ficheiro (PDF/IMG) no storage (S3/Cloud). |
| `token_acesso` | `VARCHAR(255)` | **Unique**, Nullable | Gerado apenas após o estado mudar para **APROVADO**. |
| `id_leitor` | `BIGINT`       | **FK**, Not Null | Referência ao Leitor que efetuou a compra. |
| `id_revista` | `BIGINT`       | **FK**, Not Null | Referência à Revista adquirida. |

---

## 3.0. Tabela `Revista`

Armazena as informações principais de cada edição digital da revista.

| Campo | Tipo SQL | Restrições (Constraints) | Descrição / Regra de Negócio |
| --- | --- | --- | --- |
| `id` | `BIGINT` | **PK**, Not Null, auto_inc | Identificador único da revista. |
| `nome` | `VARCHAR(100)` | Not Null | Título da revista (ex: "Revista FITITEL 2024"). |
| `ano_lancamento` | `INT` | Not Null | Ano em que a revista foi publicada. |
| `url` | `VARCHAR(500)` | Not Null | Caminho/URL do ficheiro PDF no servidor. |
| `preco` | `DECIMAL(10,2)` | Not Null | Valor da revista (0.00 para gratuitas). |
| `qtd_paginas` | `INT` | Not Null | Total de páginas do documento. |
| `id_edicao` | `BIGINT` | **FK**, Not Null | Relaciona a revista a uma Edição específica. |
| `id_admin` | `BIGINT` | **FK**, Not Null | Identifica o administrador que fez o upload. |

---

## 4.0. Tabela `Edição`

Agrupa as revistas sob um tema ou lema específico de cada feira FITITEL.

| Campo | Tipo SQL | Restrições (Constraints) | Descrição / Regra de Negócio |
| --- | --- | --- | --- |
| `id` | `BIGINT` | **PK**, Not Null, auto_inc | Identificador único da edição. |
| `numero` | `INT` | Not Null | Número da edição (ex: 1, 2, 15). |
| `tema` | `VARCHAR(150)` | Not Null | Tema central da feira naquele ano. |
| `lema` | `VARCHAR(200)` | Nullable | Frase de efeito ou lema daquela edição. |

---

## 5.0. Tabela `Página`

Detalha o conteúdo interno de cada revista, focando nos projetos expostos.

| Campo | Tipo SQL | Restrições (Constraints) | Descrição / Regra de Negócio |
| --- | --- | --- | --- |
| `id` | `BIGINT` | **PK**, Not Null, auto_inc | Identificador único da página. |
| `num_pagina` | `INT` | Not Null | O número físico da página no PDF. |
| `nome_projeto` | `VARCHAR(150)` | Nullable | Nome do projeto tecnológico descrito na página. |
| `id_revista` | `BIGINT` | **FK**, Not Null | Revista à qual a página pertence. |

---

## 6.0. Tabela `Autor_Revista`

Resolve o atributo multivalorado de autores, permitindo múltiplos autores por revista.

| Campo | Tipo SQL | Restrições (Constraints) | Descrição / Regra de Negócio |
| --- | --- | --- | --- |
| `id` | `BIGINT` | **PK**, Not Null, auto_inc | Identificador do registo de autoria. |
| `nome_autor` | `VARCHAR(150)` | Not Null | Nome completo do autor ou colaborador. |
| `id_revista` | `BIGINT` | **FK**, Not Null | Revista associada a este autor. |

---

## 7.0. Tabela `Comentário`

Gere a interação dos leitores com as páginas dos projetos.

| Campo | Tipo SQL | Restrições (Constraints) | Descrição / Regra de Negócio |
| --- | --- | --- | --- |
| `id` | `BIGINT` | **PK**, Not Null, auto_inc | Identificador único do comentário. |
| `texto` | `TEXT` | Not Null | O conteúdo do comentário em si. |
| `data_efetiv` | `TIMESTAMP` | Not Null | Data e hora em que o comentário foi publicado. |
| `id_pagina` | `BIGINT` | **FK**, Not Null | Página onde o comentário foi feito. |
| `id_leitor` | `BIGINT` | **FK**, Not Null | Leitor que escreveu o comentário. |
| `id_pai` | `BIGINT` | **FK**, Nullable | **Auto-relacionamento**: ID do comentário respondido. |

---

## 8.0. Regras de Auditoria (Campos Comuns)

Para todas as tabelas, os campos de auditoria seguem este padrão:

* **`createdAt`**: `TIMESTAMP`, Not Null, Default `CURRENT_TIMESTAMP`. (Nunca muda após a inserção).
* **`updatedAt`**: `TIMESTAMP`, Nullable. (Atualizado automaticamente em cada `UPDATE`).
* **`deletedAt`**: `TIMESTAMP`, Nullable. (Se preenchido, o registo é ignorado nas consultas normais — **Soft Delete**).
