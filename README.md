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
```sql
CREATE TABLE nome_da_tabela (campo tipo_de_dados); 
```
### Deleta tabela
```sql
DROP TABLE nome_da_tabela;
```
### Altera tabela
- Altera o nome da tabela 

```sql
ALTER TABLE nome_da_tabela
RENAME TO novo_nome_da_tabela; 
```

- Inclui uma coluna numa tabela já anteriormente criada

```sql
ALTER TABLE nome_da_tabela 
ADD nome_da_coluna tipo_de_dados; 
```

## Comandos para manipulação de dados em tabela (DML)

### Insere 

```sql 
INSERT INTO nome_da_tabela (campo(s)_que_receberão_dados) 
VALUES (valores_digitados_na_ordem_das_colunas_anteriores);
```

### Exibe 
```sql
SELECT * (todos_campos)
FROM nome_da_tabela; 
```

```sql
SELECT nome(s)_do(s)_campo(s) 
FROM nome_da_tabela;
```

#### Com restrições:
```sql
SELECT * (todos os campos (não todos os registros)) 
FROM nome_da_tabela WHERE algum_campo = dado_de_algum_registro;
```
- % desconsidera os caracteres após ele e exibe todos os registros que possuem a restrição especificada 
```sql 
SELECT * FROM nome_da_tabela 
WHERE nome like "M%";
```

```sql
SELECT * FROM nome_da_tabela 
WHERE algum_campo = 50 or algum_campo = 4 or algum_campo = 7;
```

- Retorna os registros que possuem os dados dentro do intervalo especificado entre ()
```sql
SELECT * 
FROM nome_da_tabela 
WHERE algum_campo in (50, 2, 7, 900, 4);
``` 

#### Com ordenação:
```sql
SELECT * 
FROM nome_da_tabela 
ORDER BY coluna_a_ser_ordenada ASC;
```
```sql
SELECT * 
FROM nome_da_tabela 
ORDER BY coluna_a_ser_ordenada DESC;
```

### Exclui 
```sql
DELETE from nome_da_tabela  
WHERE algum_campo = dado_de_algum_registro;
```

### Atualiza 
```sql
UPDATE nome_da_tabela
SET campo_a_ser_atualizado = novo_valor_do_registro 
WHERE campo_que_guarda_o_valor_que_identifica_o_registro_a_ser_atualizado_unicamente = valor_que_identifica_o_campo_exclusivamente
```
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

### Como fazer INNER JOIN?

INNER JOIN = LIGAÇÃO INTERNA
Resultado mostra linhas que satisfaçam a condição nas duas tabelas (não trouxe campos nulos)

```sql
SELECT * 
FROM nome_da_tabela_que_contem_a_primeira_info apelido_tabela, nome_da_tabela_que_contem_a_segunda_info apelido_tabela
WHERE apelido_tabela.campo_chave_primaria = apelido_tabela.campo_chave_estrangeira;
```
#### Entre duas tabelas
```sql
SELECT l.titulo, a.nome
FROM autor a, livro l
WHERE a.id = l.autor_id;
```
```sql
SELECT l.titulo, e.nome
FROM livro l, editora e
WHERE e.id = l.editora_id;
```
#### Entre três tabelas
```sql
SELECT l.titulo, a.nome, e.nome
FROM livro l, autor a, editora e
WHERE a.id = l.autor_id
AND e.id = l.editora_id;
```

### Convenções/Regras para o relacionamento entre tabelas
- Nome da tabela deverá ser escrito no singular (livro, autor, estilo)
- Chave primária deverá ser nomeada como id
- A chave estrangeira será nomeada como nometabelaaqualestaligada_id (autor_id, estilo_id)

### OUTER JOIN

OUTER JOIN = LEFT OUTER JOIN

### Trigger = Gatilho
```sql
CREATE TRIGGER nome_trigger AFTER ou BEFORE INSERT ou UPDATE ou DELETE ON nome_tabela 
BEGIN 
    INSERT INTO auditoria(autor_id, data, acao) 
    VALUES (new ou old.id, datetime(), "Dado Inserido"); 
END;    
```

### Função de agregação

- Count - contagem de registros
```sql
SELECT count (*) Total
FROM nome_da_tabela;
```
- Avg - média aritmética
```sql
SELECT avg(nome_do_campo) Media
FROM nome_da_tabela;
```
- Max - maior valor
```sql
select max(nome_da_coluna)
FROM nome_da_tabela;
```
- Min - menor valor
```sql
SELECT min(nome_da_coluna)
FROM nome_da_tabela;
```
### Cláusulas GROUP BY e HAVING

- GROUP BY
Agrupa os registros de acordo com um critério

Exemplo: 
```sql
SELECT count(*)
FROM editora
GROUP BY estado;
```
Retorna a quantidade de editores por estado

- HAVING
Restringe o resultado da consulta de acordo com o critério definido 
```sql
SELECT estado, count(*) total
FROM editora
GROUP BY estado
HAVING count(*) < 30;
```
### View (Visualização de dados)

#### Cria view
```sql
CREATE VIEW nome_da_view as
SELECT campo1, campo2
FROM nome_da_tabela
WHERE campo1 = valor;
```
#### Deleta View
```sql
DROP VIEW nome_da_view;
```

- Utilizada para otimizar a visualização ("atalho" para um select) de uma tabela que precisa ser consultada frequentemente.
- Evita a reconstrução de uma consulta a cada necessidade de utilização
- Não é possivel fazer atualização ou exclusão em uma view que reflita na tabela original (funciona apenas para visualização)
- É possível criar restrições com o WHERE
Exemplo: 
```sql
SELECT *
FROM livro_e_editora
WHERE nome like "Z%";
```
- É possível criar uma view a partir de uma view já existente
- É possível fazer joins entre views

### Index (Índice)

#### Cria index
```sql
CREATE INDEX idx_nome ON nome_tabela (nome_campo_muito_utilizado_em_consultas);
```
#### Deleta index

```sql
DROP INDEX idx_nome;
```
- Acelera buscas em uma tabela 
- Ao incluir e excluir dados, o índice precisa ser atualizado
- Geralmente criado pelo DBA

### Cláusula DISTINCT (Valores únicos)
- Evita que a consulta retorne com valores duplicados

```sql
SELECT DISTINCT nome_campo
FROM nome_tabela;
``` 
#### Limit
- Limita a quantidade de resgistros retornados em um SELECT

Exemplo: <br> Quais os dois livros mais caros da tabela? <br>
```sql
SELECT * 
FROM livro
ORDER BY precovenda DESC
limit 2;
```
### Subselects
- É um Select dentro de outro Select
- Usado quando há dependência de dados entre consultas distintas 
- Pode ser uma alternativa ao join

Exemplo:
<br>
- Exibe todos os livros do autor Dan Brown utilizando join

```sql
SELECT l.titulo
FROM livro l, autor a
WHERE a.id = l.autor_id
AND a.nome = "Dan Brown";
```

- Utilizando subselect
```sql
SELECT l.titulo 
FROM livro l
where l.autor_id = (
    select id
    from autor
    where nome = "Dan Brown"
);
```
- Exclui todos os livros do autor "Graciliano Ramos"
```sql
delete from livro
where id = (
    select id
    from autor
    where nome = "Graciliano Ramos"
);
```
### Transações do banco
Conjunto de operações que podem ser confirmadas ou descartadas (Ou todas as operações são realizadas ou nenhuma é)
```sql
begin transaction;
INSERT INTO nome_tabela(campos) 
VALUES (valores);
rollback; ou
commit;
```

## Comandos sqlite
- sqlite3 nome_do_banco.sqlite - Cria banco de dados
- .tables - Lista tabelas criadas no banco 
- .schema - Exibe a estrutura de todas as tabelas criadas
- .schema nome_tabela - Exibe a estrutura da tabela especificada
- .headers on - Habilita a exibição das colunas quando for feito um select 

### Funções

- ifnull
Mostra uma mensagem no registro de um campo ao invés de "null"

- length
Mostra o tamanho de uma string

- lower
Mostra uma string somente com letras minúsculas

- upper
Mostra  uma string somente com letras maiúsculas

- substr(8, 3)
Seleciona e mostra strings a partir de uma determinada posição.  O primeiro parâmetro representa a posição e o segundo a quantidade de strings que serão exibidas após a posição.

- random()
Gera números aletários

- replace()
Substitui um parâmetro por outro

- round(x)
Arredonda um valor decimal de acordo com a quantidade de casas passada no parâmetro

- trim(), rtrim(), ltrim()
Remove espaços do ínicio e do fim de uma string, do fim e do ínicio (reespectivamente)

- typeoff
Retorna o tipo de dado

- datetime();
Mostra a data atual

- select sqlite_version();
Mostra a versão do sqlite
