# Aprenda sql do zero!
Aprenda e domine a linguagem padrão para trabalho com Banco de Dados! Curso TOTALMENTE PRÁTICO, abordagem mão na massa! <br>
<a href="https://www.udemy.com/course/aprenda-sql-do-zero"> Curso disponível na Udemy </a>

## Tipos de dados

- text (texto)
- varchar() (variable character - conjuntos de caracteres limitado ao valor colocado entre parênteses)
- integer (inteiro)
- real ou number (conj. números reais)
- date (data)
- boolean (boleano) (lógico - verdadeiro ou falso)

## Comandos para definição de estrutura em tabela (DDL)

### Cria tabela
- CREATE TABLE nome_da_tabela (campo tipo_de_dados); - Cria tabela
### Deleta tabela
- DROP TABLE nome_da_tabela; - Deleta tabela
### Altera tabela
- ALTER TABLE nome_da_tabela rename to novo_nome_da_tabela; - Altera o nome da tabela 
- ALTER TABLE nome_da_tabela add nome_da_coluna tipo_de_dados; - Inclui uma coluna numa tabela já anteriormente criada

## Comandos para manipulação de dados em tabela (DML)

### Insere 
- INSERT INTO nome_da_tabela (campo(s)_que_receberão_dados) VALUES (valores_digitados_na_ordem_das_colunas_anteriores);

### Exibe 
- SELECT * (todos_campos) FROM nome_da_tabela; 
- SELECT nome(s)_do(s)_campo(s) FROM nome_da_tabela;

#### Com restrições:
- SELECT * (todos os campos (não todos os registros)) FROM nome_da_tabela WHERE algum_campo = dado_de_algum_registro;
- SELECT * FROM nome_da_tabela WHERE nome like "M%"; % desconsidera os caracteres após ele e exibe todos os registros que possuem a restrição especificada 
- SELECT * FROM nome_da_tabela WHERE algum_campo = 50 or algum_campo = 4 or algum_campo = 7; 
- SELECT * FROM nome_da_tabela WHERE algum_campo in (50, 2, 7, 900, 4); retorna os registros que possuem os dados dentro do intervalo especificado entre ()

#### Com ordenação:
- SELECT * FROM nome_da_tabela ORDER BY coluna_a_ser_ordenada ASC;
- SELECT * FROM nome_da_tabela ORDER BY coluna_a_ser_ordenada DESC;

### Exclui 
- DELETE from nome_da_tabela WHERE algum_campo = dado_de_algum_registro;

### Atualiza 
- UPDATE nome_da_tabela
SET campo_a_ser_atualizado = novo_valor_do_registro
WHERE campo_que_guarda_o_valor_que_identifica_o_registro_a_ser_atualizado_unicamente = valor_que_identifica_o_campo_exclusivamente

## Ligações
Para evitar redundância ou perda de dados por erro no cadastro, são criadas tabelas individuais onde o dado é escrito somente uma vez e identificado com um código único (chave primária). O código único pode ser referenciado por outras tabelas que necessitem do dado que o código identifica exclusivamente. Dessa forma, evita-se que seja necessário cadastrar uma mesma informação várias vezes. Como exemplo, numa tabela livros, não será necessário escrever num campo "autor" o nome dele caso exista uma tabela "autores" que possua o nome do autor e um código que identifique ele unicamente. Nesse cenário, é possível, na tabela livros, usar o campo "código do autor" e criar um relacionamento entre as tabelas livros e autores. Onde nesse relacionamento o campo "codigo do autor" na tabela livros é uma chave estrangeira já que está ligado ao campo codigo (chave primária) da tabela "autores"

### Chave primária: 
Campo que torna um registro único. Um campo, código, se for restringido como sendo uma chave primária, não poderá guardar registros (linhas) que possuam o mesmo valor. O valor de cada registro do campo será exclusivo.

### Chave estrangeira: 
Ligação de um campo (código do autor) de uma tabela (livros) à chave primaria (codigo) de outra tabela (autores). 

### Como resolver problemas envolvendo várias tabelas?
- Atenção a pergunta que precisa ser respondida!!! "Como exibir uma lista com o nome do livro e o nome do autor?"
- Em quais tabelas estão as repostas? livro e autor
- Como essas tabelas se ligam? Quais campos conectam uma tabela a outra? (autor_id (livro)(chave estrangeita) e id (autor)(chave primária))

### Como fazer JOIN?
- SELECT * 
FROM nome_da_tabela_que_contem_a_primeira_info apelido_tabela, nome_da_tabela_que_contem_a_segunda_info apelido_tabela
WHERE apelido_tabela.campo_chave_primaria = apelido_tabela.campo_chave_estrangeira;

#### Entre duas tabelas
SELECT l.titulo, a.nome
FROM autor a, livro l
WHERE a.id = l.autor_id;

SELECT l.titulo, e.nome
FROM livro l, editora e
WHERE e.id = l.editora_id;

#### Entre três tabelas

SELECT l.titulo, a.nome, e.nome
FROM livro l, autor a, editora e
WHERE a.id = l.autor_id
AND e.id = l.editora_id;

### Convenções/Regras para o relacionamento entre tabelas
- Nome da tabela deverá ser escrito no singular (livro, autor, estilo)
- Chave primária deverá ser nomeada como id
- A chave estrangeira será nomeada como nometabelaaqualestaligada_id (autor_id, estilo_id)

### Função de agregação

- Count - contagem de registros
SELECT count (*) Total
FROM nome_da_tabela;

- Avg - média aritmética
SELECT avg(nome_do_campo) Media
FROM nome_da_tabela;

## Comandos sqlite
- sqlite3 nome_do_banco.sqlite - Cria banco de dados
- .tables - Lista tabelas criadas no banco 
- .schema - Exibe a estrutura de todas as tabelas criadas
- .schema nome_tabela - Exibe a estrutura da tabela especificada
- .headers on - Habilita a exibição das colunas quando for feito um select 
