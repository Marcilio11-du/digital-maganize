# Modelo Entidade Relacionamento e Modelo Relacional

---

## 1.0. MER - Modelo Entidade Relacionamento

### Entidades (Atributos)

**Leitor** (<u>id</u>, nome, data_nascimento, email, género, palavra-passe) <br>
**Revista** (<u>id</u>, nome, ano_lançamento, edição, url, autores*, preço, quantidade_páginas, tema_edição, lema_edição) <br>
**Página** (<u>id</u>, numero_página, nome_projeto) <br>
**Pagamento** (<u>id</u>, método_pagamento, data_pagamento, url_comprovativo, estado_pagamento, token_acesso) <br>
**Administrador** (Leitor) <br>
**Comentário** (<u>id</u>, texto, data_efetividade)



### Relacionamentos e Cardinalidades

- Leitor 1 : N Pagamento - Um leitor pode ter vários registos de pagamento.
- Pagamento N : 1 - Revista - Vários pagamentos diferentes podem referenciar a mesma edição.
- Revista 1 : N - Página - Uma revista contém muitas páginas.
- Página 1 : N Comentário - Uma página recebe vários comentários.
- Leitor 1 : N Comentário - Um leitor escreve vários comentários.
- Administrador 1 : N Revista - Um admin faz o upload de várias revistas.
- Comentário (Pai) 1 : N Comentário (Filho) — Relacionamento Unário/Recursivo

---

## 2.0. MR - Modelo Relacional

Após executado o MER e feito o devido mapeamento para o MR, obtivemos os seguintes resultados a nível de tabelas:

**Leitor** (<u>id</u>, p_nome, sb_nome, data_nascimento, email, género, palavra-passe) <br>
**Administrador** (Leitor) <br>
**Revista** (<u>id</u>, nome, ano_lançamento, url, preço, quantidade_páginas, id_edição, id_administrador) <br>
**Autor_Revista** (<u>id</u>, nome_autor, id_revista) <br>
**Edição** (<u>id</u>, número, tema, lema) <br>
**Página** (<u>id</u>, numero_página, nome_projeto, id_revista) <br>
**Pagamento** (<u>id</u>, método_pagamento, data_pagamento, url_comprovativo, estado_pagamento, token_acesso, id_leitor, id_revista) <br>
**Comentário** (<u>id</u>, texto, data_efetividade, id_página, id_leitor, id_cometário_pai)

**Nota**: Para garantir a rastreabilidade e a integridade referencial do sistema, todas as entidades 
implementam o padrão de Auditoria de Dados. Os atributos createdAt e updatedAt permitem monitorizar o histórico de criação e
modificação de cada registo. Além disso, foi adotada a estratégia de Soft Delete através do atributo deletedAt.

**Leitor** (<u>id</u>, p_nome, sb_nome, data_nascimento, email, género, palavra-passe, createdAt, updatedAt, deletedAt) <br>
**Administrador** (Leitor) <br>
**Revista** (<u>id</u>, nome, ano_lançamento, url, preço, quantidade_páginas, id_edição, id_administrador, createdAt, updatedAt, deletedAt) <br>
**Autor_Revista** (<u>id</u>, nome_autor, id_revista, createdAt, updatedAt, deletedAt) <br>
**Edição** (<u>id</u>, número, tema, lema, createdAt, updatedAt, deletedAt) <br>
**Página** (<u>id</u>, numero_página, nome_projeto, id_revista, createdAt, updatedAt, deletedAt) <br>
**Pagamento** (<u>id</u>, método_pagamento, data_pagamento, url_comprovativo, estado_pagamento, token_acesso, id_leitor, id_revista, createdAt, updatedAt, deletedAt) <br>
**Comentário** (<u>id</u>, texto, data_efetividade, id_página, id_leitor, id_cometário_pai, createdAt, updatedAt, deletedAt)






