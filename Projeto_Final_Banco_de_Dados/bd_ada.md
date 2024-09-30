### Grupo:

- Luiza Souza Simões
- Matheus Bandeira
- Zibia Ribeiro
- José Marchesi
- Antonino Barria



### Modelagem e normalização de bancos de dados relacionais

###### 1. Ainda sem fazer normalizações, apresente o modelo conceitual deste esboço oferecido pelo gestor, destacando atributos chaves e multivalorados, caso existam, e apresentando também a cardinalidade dos relacionamentos.

![Modelo Conceitual.jpg](https://github.com/zemarchezi/SantanderCoders_DataScience/blob/main/Projeto_Final_Banco_de_Dados/Modelo%20Conceitual.jpg)


###### 2. Agora apresente um modelo lógico que expresse as mesmas informações e relacionamentos descritos no modelo original, mas decompondo-os quando necessário para que sejam respeitadas as 3 primeiras formas normais. Destaque atributos chaves e multivalorados, caso existam, e apresente também a cardinalidade dos relacionamentos.

![Modelo Lógico.jpg](https://github.com/zemarchezi/SantanderCoders_DataScience/blob/main/Projeto_Final_Banco_de_Dados/Modelo%20L%C3%B3gico.jpg)

### Consultas SQL simples e complexas em um banco de dados postgres

###### 3. Liste os nomes de todos os produtos que custam mais de 100 reais, ordenando-os primeiramente pelo preço e em segundo lugar pelo nome. Use alias para mostrar o nome da coluna nome como "Produto" e da coluna preco como "Valor". A resposta da consulta não deve mostrar outras colunas de dados.

SELECT nome AS Produto, preco AS Valor

FROM produtos  

WHERE preco > 100 

ORDER BY Valor, Produto;



###### 4. Liste todos os ids e preços de produtos cujo preço seja maior do que a média de todos os preços encontrados na tabela "produtos".

SELECT id, preco FROM produtos 

WHERE preco > (SELECT AVG(preco) FROM produtos);


###### 5. Para cada categoria, mostre o preço médio do conjunto de produtos a ela associados. Caso uma categoria não tenha nenhum produto a ela associada, esta categoria não deve aparecer no resultado final. A consulta deve estar ordenada pelos nomes das categorias.

SELECT c.nome AS Categoria, AVG(p.preco) AS Preco_Medio

FROM categorias c

INNER JOIN produtos_categorias pc ON c.id = pc.categoria_id

INNER JOIN produtos p ON p.id = pc.produto_id

GROUP BY Categoria;


### Inserções, alterações e remoções de objetos e dados em um banco de dados postgres

###### 6. Com o objetivo de demonstrar o seu conhecimento através de um exemplo contextualizado com o dia-a-dia da escola, utilize os comandos do subgrupo de funções DDL para construir o banco de dados simples abaixo, que representa um relacionamento do tipo 1,n entre as entidades "aluno" e "turma":

* Criar uma tabela chamada "turma"

CREATE TABLE turma ( `<br>`

    id_turma INT PRIMARY KEY AUTO_INCREMENT,`<br>`

    nome_turma VARCHAR(100) NOT NULL`<br>`

);

* Cria uma tabela "aluno" com uma chave estrangeira do id da turma

CREATE TABLE aluno ( 

    id_aluno INT PRIMARY KEY AUTO_INCREMENT,

    nome_aluno VARCHAR(100) NOT NULL,

    aluno_alocado BOOLEAN,

    id_turma INT,

    FOREIGN KEY (id_turma) REFERENCES turma(id_turma)

);



###### 7. Agora que você demonstrou que consegue ser mais do que um simples usuário do banco de dados, mostre separadamente cada um dos códigos DML necessários para cumprir cada uma das etapas a seguir:

a) Inserir pelo menos duas turmas diferentes na tabela de turma; 

b) Inserir pelo menos 1 aluno alocado em cada uma destas turmas na tabela aluno (todos com NULL na coluna aluno_alocado); 

c) Inserir pelo menos 2 alunos não alocados em nenhuma turma na tabela aluno (todos com NULL na coluna aluno_alocado); 

d) Atualizar a coluna aluno_alocado da tabela aluno, de modo que os alunos associados a uma disciplina recebam o valor True e alunos não associdos a nenhuma disciplina recebam o valor False para esta coluna.


a)

INSERT INTO turma (id_turma, nome_turma) 

VALUES (1, 'Turma A');

INSERT INTO turma (id_turma, nome_turma) 

VALUES (2, 'Turma B');


b)

INSERT INTO aluno (id_aluno, nome_aluno, aluno_alocado, id_turma) 

VALUES (1, 'João Silva', NULL, 1);

INSERT INTO aluno (id_aluno, nome_aluno, aluno_alocado, id_turma) 

VALUES (2, 'Maria Souza', NULL, 2);


c)

INSERT INTO aluno (id_aluno, nome_aluno, aluno_alocado, id_turma) 

VALUES (3, 'Carlos Pereira', NULL, NULL);

INSERT INTO aluno (id_aluno, nome_aluno, aluno_alocado, id_turma) 

VALUES (4, 'Ana Fernandes', NULL, NULL);


d)

UPDATE aluno 

SET aluno_alocado = TRUE 

WHERE id_turma IS NOT NULL;

UPDATE aluno 

SET aluno_alocado = FALSE 

WHERE id_turma IS NULL;
