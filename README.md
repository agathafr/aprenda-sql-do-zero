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

### Exclui 
- DELETE from nome_da_tabela WHERE algum_campo = dado_de_algum_registro;

### Atualiza 


## Comandos sqlite
- sqlite3 nome_do_banco.sqlite - Cria banco de dados
- .tables - Lista tabelas criadas no banco 
- .schema - Exibe a estrutura de todas as tabelas criadas
- .schema nome_tabela - Exibe a estrutura da tabela especificada
- .headers on - Habilita a exibição das colunas quando for feito um select 
