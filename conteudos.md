## O que vamos aprender?

Agora que você já sabe como realizar um CRUD profissional com as _queries_ e a utilizar as principais funções no MySQL. Está na hora de impulsionar ainda mais o seu conhecimento com recursos poderosos do SQL, que serão muito utilizados ao longo do curso!

No dia de hoje, você irá aprofundar e colocar em prática o que viu anteriormente sobre **relacionamento entre entidades** com o comando **JOIN**, que o permitirá unir duas tabelas diferentes baseadas em uma propriedade em comum.

# Você será capaz de:

- Utilizar queries envolvendo mais de uma tabela;
- Realizar junções entre duas tabelas relacionadas com o JOIN;
- Entender as principais diferenças entre INNER, LEFT, RIGHT e SELF joins;
- Dar um apelido (alias) para as nossas entidades com o AS.

## Porque isso é importante?

No módulo de Front-end, entendemos a importância de utilizar as boas práticas do _Clean Code_ para produzirmos códigos que, além de solucionar os problemas a mão, também sejam limpos, organizados e fáceis de ler e compreender. No módulo de Back-end, não é diferente!

Suponha que você seja contratado como desenvolvedor Full-stack por uma grande empresa, e seja encarregado de gerenciar um banco de dados extenso e altamente complexo. Agora, imagine que você precise encontrar um dado em uma tabela semi-infinita com mais de 50 colunas. Aterrorizante, não é mesmo?

Com o JOIN, você conseguirá dividir grandes entidades em menores, que complementem o significado uma das outras e melhorarão sua organização e produtividade. Dessa forma, você será capaz de criar bancos de dados cada vez melhores!

![Dados estruturados](http://www.skysync.com/wp-content/uploads/2020/12/Unstructured-VS-Structured-Data-Image-New-Branding.png "Dados estruturados")
*Dados desestruturados VS estruturados*

## Conteúdos

# Entendendo o JOIN

O **JOIN** (“juntar” em inglês) nada mais é que uma cláusula capaz de criar relacionamentos entre duas entidades, baseando-se em uma propriedade comum. Mais especificamente, podemos unir resultados de duas ou mais tabelas quando suas linhas e colunas forem equivalentes. A ferramenta, portanto, facilita a consulta de tabelas que, apesar de separadas, complementam o sentido uma das outras.

Existem diversos tipos de Join, e é muito importante saber quando e qual deles utilizar. Ao todo, a linguagem SQL nos dá cinco opções:
- **INNER JOIN**;
- **RIGHT JOIN**;
- **LEFT JOIN**;
- **OUTER** ou **FULL JOIN**;
- **CROSS JOIN**.

Mais adiante, você aprenderá os detalhes e a necessidade das cláusulas mais utilizadas.

![Trybe joins](https://i.imgur.com/qvD5TYD.png "Trybe joins")
*Diagramas dos tipos de JOIN*

# Unindo tabelas com o INNER JOIN

Para iniciarmos nossa jornada com o JOIN, vamos tomar como exemplo as seguintes tabelas, **Artists** e **Albums**:

![Exemplo tabelas](https://i.imgur.com/fFw6CkO.png "Exemplo tabelas")
*Artistas e seus álbums correspondentes*

Como você pode observar, as tabelas já possuem uma conexão implícita, pois as colunas "id" e "artist_id" possuem os mesmos valores e servirão de referência para fazermos a junção delas. Bora?

Para começar, faremos um SELECT de todos os valores de uma das tabelas que queremos unir, como, por exemplo, "Artists":

```
SELECT * FROM meu_banco_de_dados.artists
```

Em seguida, escrevemos **INNER JOIN**, seguido do nome da tabela a que queremos juntar:

```
SELECT * FROM meu_banco_de_dados.artists
INNER JOIN meu_banco_de_dados.albums
```

Mas não para aí, pois ainda precisamos dizer ao MySQL como, exatamente, queremos que essa junção seja feita. Nesse caso, queremos unir elas quando o **id** de Artists for igual ao **artist_id** de Albums:

```
SELECT * FROM meu_banco_de_dados.artists
INNER JOIN meu_banco_de_dados.albums
ON (meu_banco_de_dados.artists.id = meu_banco_de_dados.albums.artist_id);
```
*A palavra ON é uma sintaxe nova para especificar condições ou colunas para unir, similar ao WHERE*

Para tornar o script acima mais legível, podemos utilizar o **AS** (ou alias), que nos permite apelidar as tabelas que queremos juntar, evitando a repetição de palavras:

```
SELECT * FROM meu_banco_de_dados.artists AS ART
INNER JOIN meu_banco_de_dados.albums AS ALB
ON (ART.id = ALB.artist_id);
```

**Dica:** Quando estivermos apelidando entidades, é sempre recomendado utilizar letras ou abreviações curtas. Utilize nomes mais descritivos só quando necessário. Adicionalmente, também é possível omitir a palavra-chave *AS* antes do apelido.

Executando a _query_ acima, obtemos um resultado similar ao de baixo:

![Tabelas unidas](https://i.imgur.com/SfNTPnc.png "Tabelas unidas")

Esse tipo de join é o que chamamos de **INNER JOIN**, pois ele retorna apenas as linhas que ambas tabelas tem em comum (que, neste caso, são todas). Como esse é o tipo padrão, é possível a omissão da palavra-chave INNER antes do comando.

# Unindo tabelas de tamanhos diferentes

Mas você deve estar se perguntando: "E se eu tivesse um artista ou álbum a mais em uma das tabelas?" Pois bem! É aí que entram os **LEFT** e **RIGHT** joins (inglês para _esquerda_ e _direita_, respectivamente).

Sempre que você estiver comparando duas tabelas no MySQL, o output mostrará as duas lado a lado, uma na esquerda e outra na direita. Esse tipo de join nos permite retornar todos os valores de uma tabela específica, mesmo que não exista um valor correspondente do outro lado.

Confira os exemplos a seguir:

![Exemplo tabelas](https://i.imgur.com/kkRe52f.png "Exemplo tabelas")
*Agora a tabela Albums possui um novo álbum, mas sem um artista correspondente.*

Para unir as tabelas sem omitir nenhuma fileira, podemos utilizar tanto o LEFT quanto o RIGHT. Isto só dependerá de qual tabela você escolher selecionar primeiro.

Utilizando o **LEFT JOIN**, poderíamos escrever nossa _query_ assim:

```
SELECT * FROM meu_banco_de_dados.albums AS ALB
LEFT JOIN meu_banco_de_dados.artists AS ART
ON (ALB.artist_id = ART.id);
```

E o resultado:

![Tabelas unidas sem omissão](https://i.imgur.com/61ziS4P.png "Tabelas unidas sem omissão")

Isso funciona, pois a tabela selecionada no SELECT sempre aparecerá primeiro, ou seja, na esquerda do output. Portanto, o **LEFT JOIN** consegue retornar todos os dados da tabela "Albums".

Para fazermos o mesmo com o **RIGHT JOIN**, teríamos que inverter a tabela selecionada:

```
SELECT * FROM meu_banco_de_dados.artists AS ART
RIGHT JOIN meu_banco_de_dados.albums AS ALB
ON (ART.id = ALB.artist_id);
```
![Tabelas unidas sem omissão](https://i.imgur.com/WJ0xpoB.png "Tabelas unidas sem omissão")

Agora com a tabela "Artists" na esquerda, conseguimos ver todas as instâncias de "Albums" na direita utilizando o **RIGHT JOIN**.

Caso tenha ficado com alguma dúvida, não se preocupe. Teremos tempo para praticar ao final do dia. 🚀

# E o SELF JOIN, para que serve?

Você aprendeu como consultar partes de duas tabelas com o JOIN. Entretanto, em alguns casos mais específicos, pode fazer sentido comparar várias partes de uma mesma entidade. O conceito do **SELF JOIN** nos ajuda a fazer justamente isso.

Para os exemplos, vamos utilizar o _schema_ do sakila para comparar as linhas da tabela "film".

Supondo que você queira saber o título e a duração de todos os filmes com a mesma taxa de aluguel, seria necessário comparar a tabela consigo mesma. Poderíamos começar escrevendo um JOIN com as propriedades necessárias:

```
SELECT F.title, F.length, F.rental_rate
FROM sakila.film AS F
WHERE F.rental_rate = F.rental_rate
```

“Mas calma aí, é realmente possível comparar as duas fileiras dessa forma?” Para podermos comparar duas partes de uma única entidade, é preciso apelidar a tabela *duas* vezes. Primeiro, apelidaremos a primeira instância da tabela de **T1**:

```
SELECT T1.title, T1.length
FROM sakila.film AS T1
...
```

Para criarmos uma “cópia”, ou segunda instância da mesma tabela, vamos repetir os passos anteriores:

```
SELECT T1.title, T1.length, T2.title, T2.length
FROM sakila.film AS T1, sakila.film AS T2
...
```

Finalmente, podemos comparar as taxas de aluguel da tabela consigo mesmas:

```
SELECT T1.title, T1.length, T2.title, T2.length
FROM sakila.film AS T1, sakila.film AS T2
WHERE T1.rental_rate = T2.rental_rate;
```

Executando a _query_ acima, obtemos a seguinte resposta:

![Resultado self join](https://i.imgur.com/aSGHSZ5.png "Resultado self join")

Voilà! Agora podemos comparar todos os filmes com aqueles que possuem a mesma taxa de aluguel. No caso da figura, o "Academy Dinosaur" aparece primeiro.

**Importante**: note que o **SELF JOIN** não é um tipo de Join em si, mas uma forma de escrever nossas _queries_ para obter os resultados desejados. Quando estiver comparando uma entidade com ela mesma, utilize o WHERE.

## Para fixar

Para consolidar o conceito de SELF JOIN, realize o seguinte exercício:

1. Na mesma tabela, selecione as colunas "title" e "rating";

2. Crie uma segunda instância da tabela com o *alias*: **AS**;

3. Compare as duas instâncias retornando "title" e "rating" para os filmes com a mesma duração.

## Vamos praticar!

Vamos bater um papo sobre SQL? Hora da aula ao vivo! Vamos para o Slack, onde o link estará disponível. 

## Exercícios
# Agora a prática

Que tal consolidar os conhecimentos adquiridos no dia com alguns exercícios práticos? Para os enunciados 1 até o 7, utilizaremos o banco de dados *sakila*. Lembre-se de identificar onde estão localizadas as colunas antes de começar a escrever sua _query_.

**Exercício 1:** Utilizando o INNER JOIN, desenvolva uma _query_ que mostre o **nome do ator**, **id do ator** e **id do filme** em que ele estreiou, unindo as tabelas "actor" e "film_actor" através do id do ator;

**Exercício 2:** Utilizando o INNER JOIN, desenvolva uma _query_ que mostre o **último nome** do e a **data de aluguel**, unindo as tabelas "customer" e "rental" através do id do cliente;

**Exercício 3:** Utilizando o INNER JOIN, desenvolva uma _query_ que mostre o **título do filme** e o **id da categoria**, unindo as tabelas "film" e "film_category" através do id do filme;

**Exercício 4:** Utilizando o INNER JOIN, desenvolva uma _query_ que mostre o nome da cidade e do país, unindo as tabelas "city" e "country" através do id do país. Retorne apenas os primeiros **5** resultados;

**Exercício 5:** Utilizando o **LEFT** ou **RIGHT JOIN**, una os distritos em "address" e o nome dos clientes que residem neles em "customers" sem omitir nenhuma linha;

**Exercício 6:** Utilizando o **LEFT** ou **RIGHT JOIN**, una os números telefônicos em "address" e o nome completo de seus respectivos donos em "customers" sem omitir nenhuma linha de ambas colunas;

**Exercício 7:** Desenvolva uma _query_ que mostre o **nome do ator**, **id do filme**, e o **titulo do filme** unindo as tabelas "actor", "film_actor" e "actor", ou seja, fazendo dois INNER JOINs;


**Exercício 8:** Modifique o JOIN do exercício 3 para mostrar apenas o **título do filme** e a **categoria**, unindo as tabelas "film", "film_category" e "category" através do id de ambos;

**Exercício 9:** Utilizando o SELF JOIN, desenvolva uma _query_ que retorne a **duração do aluguel** e o **id do filme** para os filmes com a mesma duração. Retorne apenas o id do filme da instância um, e a duração do aluguel da instância dois;

# Bônus

**Exercício 10:** Utilizando o SELF JOIN, desenvolva uma _query_ que retorne o **título**, **duração** e **classificação** de todos os filmes que tem suas classificações iguais.

**Exercício 11:** Utilizando o SELF JOIN, retorne o **endereço** e **id da cidade** para todos os endereços com o mesmo distrito.

## Recursos adicionais (opcional)

- [Quer conhecer os outros tipos de JOIN? Confira no blog da Trybe!](https://blog.betrybe.com/sql/sql-join/)

- [Entenda a diferença entre chave primaria e chave estrangeira](https://www.devmedia.com.br/sql-aprenda-a-utilizar-a-chave-primaria-e-a-chave-estrangeira/37636)

- ["ON" vs "WHERE", são a mesma coisa?](https://www.ti-enxame.com/pt/sql/no-sql-mysql-qual-e-diferenca-entre-e-where-em-uma-instrucao-de-juncao/969998723/)


