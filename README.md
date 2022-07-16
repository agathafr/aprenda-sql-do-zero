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

### Comando para criar tabela
- CREATE TABLE nome_da_tabela (campo tipo_de_dados); - Cria tabela
### Comando para deletar tabela
- DROP TABLE nome_da_tabela; - Deleta tabela
### Comandos para alterar tabela
- ALTER TABLE nome_da_tabela rename to novo_nome_da_tabela; - Altera o nome da tabela 
- ALTER TABLE nome_da_tabela add nome_da_coluna tipo_de_dados; - Inclui uma coluna numa tabela já anteriormente criada

## Comandos sqlite
- sqlite3 nome_do_banco.sqlite - Cria banco de dados
- .tables - Lista tabelas criadas no banco 
- .schema - Exibe a estrutura de todas as tabelas criadas
- .schema nome_tabela - Exibe a estrutura da tabela especificada
