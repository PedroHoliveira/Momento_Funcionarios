# Momento_Funcionarios
Atividade de Banco de Dados

1 - Inclua suas próprias informações no departamento de tecnologia da empresa.

INSERT INTO funcionarios (primeiro_nome, sobrenome, email, telefone, dataContratacao, ocupacao_id, salario, departamento_id) VALUES ('Pedro', 'Oliveira', 'pedro.oliveira@momento.org', '123 456 789 000', '2022-06-07', (SELECT ocupacao_id FROM ocupacoes WHERE ocupacao_title LIKE '%Desenvolvedor Web%'), 2500.00, (SELECT departamento_id FROM departamento WHERE departamento_name LIKE '%Tecnologia%'));

<hr>

2 - A administração está sem funcionários. Inclua os outros elementos do seu grupo do demoday no departamento de administração.

INSERT INTO funcionarios(primeiro_nome, sobrenome, email, telefone, dataContratacao, ocupacao_id, salario, departamento_id)
VALUES ('Camily', 'Vitoria', 'Cami.vit@momento.org', '11 304343434', '2012-06-12',
(SELECT ocupacao_id FROM ocupacoes WHERE ocupacao_title LIKE '%Vice-presidente de administração%'), 15200.00, (SELECT departamento_id FROM departamento WHERE departamento_name LIKE '%Admnistração%')),('Giullia', 'Maria', 'Maria.Giullia@momento.org', '11 305563434', '2021-05-12', (SELECT ocupacao_id FROM ocupacoes WHERE ocupacao_title LIKE '%Assistente Administrativo%'), 1200.00, (SELECT departamento_id FROM departamento WHERE departamento_name LIKE '%Admnistração%')), ('Diego', 'Santos', 'Diego.santos@momento.org', '11 98963434', '1998-09-20', (SELECT ocupacao_id FROM ocupacoes WHERE ocupacao_title LIKE '%Assistente Administrativo%'), 1200.00, (SELECT departamento_id FROM departamento WHERE departamento_name LIKE '%Admnistração%'));

<hr>

3 - Agora diga, quantos funcionários temos ao total na empresa?

SELECT COUNT(*) FROM funcionarios

44 Funcionários 

<hr>

4 - Quantos funcionários temos no departamento de finanças?

SELECT COUNT(funcionarios.primeiro_nome) FROM funcionarios INNER JOIN departamento WHERE departamento.departamento_name LIKE '%Finanças%' AND departamento.departamento_id = funcionarios.departamento_id;

6 funcionários

<hr>

5 - Qual a média salarial do departamento de tecnologia?

SELECT ROUND(AVG(funcionarios.salario),2) FROM funcionarios INNER JOIN departamento WHERE departamento.departamento_name LIKE '%Tecnologia%' AND funcionarios.departamento_id = departamento.departamento_id;

5216.67$

<hr>

6 - Quanto o departamento de Transportes gasta em salários?

SELECT SUM(funcionarios.salario) FROM departamento INNER JOIN funcionarios WHERE departamento.departamento_name LIKE '%Transporte%' AND funcionarios.departamento_id = departamento.departamento_id;

41,200.00$

<hr>

7 - Um novo departamento foi criado. O departamento de inovações. Ele será locado no Brasil. Por favor, adicione-o no banco de dados.

INSERT INTO departamento (departamento_name, posicao_id) VALUES ('tristeza', (SELECT posicao_id FROM posicao WHERE pais_id LIKE '%BR%' AND cidade LIKE '%São Paulo%'));

<hr>

8 - Novos Funcionários!
Três novos funcionários foram contratados para o departamento de inovações. Por favor, adicione-os: William Ferreira, casado com Inara Ferreira, possui um filho chamado Gabriel que tem 4 anos e adora brincar com cachorros. Ele será programador.Já a Fernanda Lima, que é casada com o Rodrigo, não possui filhos. Ela vai ocupar a posição de desenvolvedora.  Por último, a Gerente do departamento será Fabiana Raulino. Casada, duas filhas (Maya e Laura). 

O salário de todos eles será a média salarial dos departamentos de administração e finanças. 
Query com a resposta

INSERT INTO funcionarios(primeiro_nome, sobrenome, email, telefone, dataContratacao, ocupacao_id, salario, departamento_id) VALUES ('William', 'Ferreira', 'ferreira.will@momento.org', '688 695 4949', '2022-05-28', (SELECT ocupacao_id FROM ocupacoes WHERE ocupacao_title LIKE '%Desenvolvedor Web%'), (SELECT * FROM media), (SELECT departamento_id FROM departamento WHERE departamento_name LIKE '%tristeza%')), ('Fernanda', 'Lima', 'Lima.fern@momento.org', '788 695 658', '2022-05-28', (SELECT ocupacao_id FROM ocupacoes WHERE ocupacao_title LIKE '%Desenvolvedor Web%'), (SELECT * FROM media), (SELECT departamento_id FROM departamento WHERE departamento_name LIKE '%tristeza%')), ('Fabiana', 'Raulino', 'fabi.Rau@momento.org', '688 695 4949', '2022-05-28', (SELECT ocupacao_id FROM ocupacoes WHERE ocupacao_title LIKE '%Gerente de Finanças%'), (SELECT * FROM media), (SELECT departamento_id FROM departamento WHERE departamento_name LIKE '%tristeza%'));

<hr>

9 - Informe todas as regiões em que a empresa atua acompanhadas de seus países.

SELECT paises.pais_name AS Pais, regiao.regiao_name FROM paises INNER JOIN regiao WHERE paises.regiao_id = regiao.regiao_id;

<hr>

10 - Joe Sciarra é filho de quem?

SELECT funcionarios.primeiro_nome, funcionarios.sobrenome FROM dependentes INNER JOIN funcionarios WHERE dependentes.funcionario_id = funcionarios.funcionario_id AND dependentes.primeiro_nome LIKE '%Joe%' AND dependentes.sobrenome LIKE '%Sciarra%';

Filho de Ismael Sciarra

<hr>

11 - Jose Manuel possui filhos?

SELECT funcionarios.primeiro_nome, dependentes.primeiro_nome FROM dependentes INNER JOIN funcionarios WHERE dependentes.funcionario_id = funcionarios.funcionario_id AND dependentes.sobrenome LIKE '%Manuel%';

Não

<hr>

12 - Qual região possui mais países?

SELECT regiao.regiao_name, COUNT(paises.regiao_id) FROM paises INNER JOIN regiao WHERE regiao.regiao_id = paises.regiao_id GROUP BY regiao.regiao_name;

<hr>

Europa
13 - Exiba o nome cada funcionário acompanhado de seus dependentes.

SELECT funcionarios.primeiro_nome, dependentes.primeiro_nome FROM funcionarios INNER JOIN dependentes WHERE funcionarios.funcionario_id = dependentes.funcionario_id

<hr>

14 - Karen Partners possui um cônjuge?

SELECT dependentes.primeiro_nome, dependentes.sobrenome FROM dependentes INNER JOIN funcionarios WHERE funcionarios.funcionario_id = dependentes.funcionario_id AND dependentes.funcionario_id = (SELECT funcionario_id FROM funcionarios WHERE primeiro_nome LIKE '%Karen%' AND sobrenome LIKE '%Partners%');

Sim, Alec

<hr>

15 - O ID da tabela de países não segue um padrão numérico. Na sua visão, qual o impacto disso no desenvolvimento do banco?

Nenhum, pois o requisito para ser uma Primary Key é não ser nulo e ser unico.
