Estudo de caso para a modelagem de dados do Back-end do "site" da Revista FITITEL.

# Estudo de caso: Revista FITITEL Digital

O Instituto de Telecomunicações, ITEL, pretende expandir a Revista da sua feira de inovação Tecnológica, a FITITEL, 
desenvolvendo uma revista DIGITAL. Para garantir uma boa performance a nível de requisições e respostas por parte do servidor,
será necessário implementar um sistema de armazenamento dos dados brutos que englobam Sistema.
A site da Revista, deverá lidar essencialmente com a **revista** e os **utilizadores**. No sistema, cada utilizador poderá ter
o seu nome completo, data de nascimento, email, género, palavra-passe e um identificador único. As revistas, possuem um nome, ano de 
lançamento, edição, URL do Pdf da revista, autores, preço, quantidade de páginas, tema da edição e o lema da referida edição.
O sistema, deverá ainda permitir o **pagamento** das revistas e cada utilizador, só poderá ler a revista inteira e efetuar o
referido pagamento. Cada pagamento possui um identificador único, método de pagamento, data de pagamento, URL do comprovante,
estado do pagamento(ex: pendente, em análise, aprovado e rejeitado) e um toke de acesso à revista. 
Haverá ainda os **administradores**, que serão os responsáveis por adicionar as revistas ao sistema. Cada administrador, deverá 
possuir todos os elementos dos utilizadores. Os utilizadores, podem ainda fazer **comentários** em páginas específicas da revista.
Cada comentário possui um texto e data de efetividade do comentário.
Cada utilizador pode pagar mais de uma revista, e uma revista, pode pertencer vários utilizadores, oq implica dizer, que
um utilizador, podes efetuar vários pagamentos, no entanto, um pagamento só pode ser efetuado por um único utilizador.
Ainda sobre a revistas, é importante referir que, um utilizador, pode fazer múltiplos comentários sobre uma página da revista e, 
ao mesmo tempo, uma página pode sofrer vários comentários pelos utilizadores.
Sabe-se que, os administradores, podem adicionar revistas ao sistema. Cada admin poderá adicionar várias revistas,
mas, uma revista só pode ser adicionada por um único administrador.