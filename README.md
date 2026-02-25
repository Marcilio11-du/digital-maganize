Este documento, estabelece um guia que contém a base conceitual para o desenvolvimento do Back-end Sistem da revista **FITITEL**.

# 1. Levantamento de requisitos/Features

---

**Descrição da ideia:** O sistema, consiste em uma aplicação web, que permite a disposição e consequente exibição das revistas
da Feira de Inovação Tecnológica do ITEL, a FITITEL. O site, permitirá observar as revistas, no entanto, apenas pra quem 
efetuou o pagamento da mesma.

## 1.1. Definição de features

### 1.1.1. Navegação contextual
>**Descrição:**
> Consiste em uma linha do tempo, interactiva que substitui uma lista estática de arquivos.
> Aumenta o tempo de permanência no site, e, transforma edições antigas em fontes de consulta recorrente.

### 1.1.2. Conteúdo "Phygital"
>**Descrição:**
>Consiste em uma forma diferenciada de disposição/exibição da revista no site, que permite abrir
>o conteúdo estático. Artigos técnicos que possuem botões pra expandir, e quem sabe, no futuro, modelos em 3D que não cabem no
>papel. Torna-se vantajoso, pois, cria a uma real necessidade de visitar o site, mesmo que já tenham a revista física, 
>pelo facto de tornar a navegação mais *performática* e intuitiva.

### 1.1.3. Sistema de comentários
>**Descrição:**
> Um sistema de comentários e anotações "sticky" sobre as páginas da revista.
> Leitores podem destacar trechos de um artigo e iniciar uma discussão ali mesmo.

### 1.1.4. Sistema de amostras
>**Descrição:**
> Em vez de "bloquear" a revista paga, o site oferece uma experiência de "degustação".
> Para desbloquear o "conhecimento profundo", ele terá de pagar.
---

## 1.2 Requisitos Funcionais

* **RF1**: O Sistema permitir que os utilizadores sejam registados no site, de modos a que possuam uma conta de utilizador;
* **RF2**: Os utilizadores (registados como não), poderão pagar observar uma *flashback* da revista. No entanto, terão de pagar para vê-la completa;
* **RF3**: Os utilizadores que efectuarem o pagamento, só poderão observar as revistas completas se, de facto, estiverem logados;
* **RF4**: O sistema deve permitir a gestão de pagamentos (integração via comprovativo ou Gateway), associando a transação à conta do utilizador e à edição específica da revista;

* **RF5**: O sistema deve possuir um painel administrativo para o upload de novas edições (PDF/Imagens) e gestão de metadados (tema do ano, autores, data);

* **RF6**: O sistema deve permitir a gestão de "Amostras" (Preview), definindo quais páginas ou secções são de acesso público e quais são restritas;

* **RF7**: O sistema deve permitir que utilizadores autenticados criem e visualizem comentários/anotações em pontos específicos das páginas (referente à feature 1.1.3);

* **RF8**: O sistema deve gerar um histórico de acessos/leituras para que o utilizador saiba onde parou a leitura de cada revista.

## 1.3 Requisitos Não Funcionais

* **RNF1**: As senhas dos utilizadores devem ser armazenadas utilizando algoritmos de hashing;

* **RNF2**: O sistema deve carregar as visualizações das revistas de forma otimizada, para garantir fluidez mesmo em ligações de internet instáveis;

* **RNF3**: O banco de dados deve garantir a integridade referencial, impedindo que um utilizador aceda a uma revista cujo pagamento não foi confirmado ou foi estornado;

* **RNF4**: A arquitetura do backend deve ser modular (seguindo boas práticas de Clean Architecture ou Layered Architecture) para permitir a futura implementação dos modelos 3D mencionados na feature 1.1.2.

# 2. Sugestões de Regras de Negócio

* **RN - Validação de Pagamento**: O acesso à revista completa só é libertado após a validação manual do administrador (via comprovativo) ou automática via API bancária.

* **RN - Sessão Única**: (Opcional) Para evitar pirataria, o sistema pode impedir que a mesma conta visualize a revista paga em mais de dois dispositivos simultaneamente.

* **RN - Expiração de Amostra**: O utilizador não logado tem acesso a, no máximo, 15% do conteúdo total de cada edição.
