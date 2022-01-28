### Gabarito dos exercícios

Lembre-se que os exercícios servem para consolidar o seu aprendizado e te ajudar a identificar as suas dúvidas! Portanto, é esperado que você trave em algum momento. Somente olhe o gabarito depois de tentar resolver o problema por algum tempo! Garanta que você entendeu tudo que está aqui, explique para "a parede" para ter certeza e, se houver dificuldade, tire sua dúvida conosco!

## Conteúdos
# E o SELF JOIN, para que serve?

### Para Fixar

Para consolidar o conceito de SELF JOIN, realize o seguinte exercício:

1. Na mesma tabela, selecione as colunas "title" e "rating". **Solução:**
```
SELECT title, rating
FROM sakila.film
...
```

2. Crie uma segunda instância da tabela com o *alias*: **AS**. **Solução:**
```
SELECT t1.title, t1.rating, t2.title, t2.rating
FROM sakila.film AS t1, sakila.film AS t2
...
```

3. Compare as duas instâncias retornando "title" e "rating" para os filmes com a mesma duração. **Solução:**
```
SELECT t1.title, t1.rating, t2.title, t2.rating
FROM sakila.film AS t1, sakila.film AS t2
WHERE t1.length = t2.length;
```

### Exercícios
# Agora a prática

1. Utilizando o INNER JOIN, desenvolva uma _query_ que mostre o **nome do ator**, **id do ator** e **id do filme** em que ele estreiou, unindo as tabelas "actor" e "film_actor" através do id do ator. **Solução:**
```
SELECT
    A.first_name, A.actor_id, F.film_id
FROM
    sakila.actor AS A
INNER JOIN
    sakila.film_actor AS F
    ON (A.actor_id = F.actor_id);
```

2. Utilizando o INNER JOIN, desenvolva uma _query_ que mostre o **último nome** do e a **data de aluguel**, unindo as tabelas "customer" e "rental" através do id do cliente. **Solução:**
```
SELECT
    C.last_name, R.rental_date
FROM
    sakila.customer as C
INNER JOIN
    sakila.rental as R
    ON (C.customer_id = R.customer_id);
```

3. Utilizando o INNER JOIN, desenvolva uma _query_ que mostre o **título do filme** e o **id da categoria**, unindo as tabelas "film" e "film_category" através do id do filme. **Solução:**
```
SELECT
    F.title, FC.category_id
FROM
    sakila.film as F
INNER JOIN
    sakila.film_category as FC
    ON (F.film_id = FC.film_id);
```

4. Utilizando o INNER JOIN, desenvolva uma _query_ que mostre o nome da cidade e do país, unindo as tabelas "city" e "country" através do id do país. Retorne apenas os primeiros **5** resultados. **Solução:**
```
SELECT
    CI.city, CO.country
FROM
    sakila.city AS CI
INNER JOIN
    sakila.country AS CO
    ON (CI.country_id = CO.country_id) LIMIT 5;
```

5. Utilizando o **LEFT** ou **RIGHT JOIN**, una os distritos em "address" e o nome dos clientes que residem neles em "customers" sem omitir nenhuma linha. **Solução:**

Com **LEFT JOIN**:
```
SELECT
    A.district, C.first_name
FROM
    sakila.address as A
LEFT JOIN
    sakila.customer as C 
    ON (A.address_id = C.address_id);
```

Com **RIGHT JOIN**:
```
SELECT
    C.first_name, A.district
FROM
    sakila.customer as C
RIGHT JOIN
    sakila.address as A
    ON (C.address_id = A.address_id);
```

6. Utilizando o **LEFT** ou **RIGHT JOIN**, una os números telefônicos em "address" e o nome completo de seus respectivos donos em "customers" sem omitir nenhuma linha de ambas colunas. **Solução:**

Com **LEFT JOIN**:

```
SELECT
	A.phone,
	CONCAT(C.first_name, ' ', C.last_name)
FROM
	sakila.address as A
LEFT JOIN
	sakila.customer as C 
    ON (A.address_id = C.address_id);
```

Com **RIGHT JOIN**:
```
SELECT
	CONCAT(C.first_name, ' ', C.last_name),
    A.phone
FROM
	sakila.customer as C
RIGHT JOIN
	sakila.address as A
    ON (C.address_id = A.address_id);
```

7. Desenvolva uma _query_ que mostre o **nome do ator**, **id do filme**, e o **titulo do filme** unindo as tabelas "actor", "film_actor" e "actor", ou seja, fazendo dois INNER JOINs. **Solução:**
```
SELECT
    A.first_name, FA.film_id, F.title
FROM
    sakila.actor AS A
INNER JOIN
    sakila.film_actor AS FA
    ON (A.actor_id = FA.actor_id)
INNER JOIN
    sakila.film AS F
    ON (FA.film_id = F.film_id);
```

8. Modifique o JOIN do exercício 3 para mostrar apenas o **título do filme** e a **categoria**, unindo as tabelas "film", "film_category" e "category" através do id de ambos. **Solução:**
```
SELECT
    F.title, C.name
FROM
    sakila.film as F
INNER JOIN
    sakila.film_category as FC
    ON (F.film_id = FC.film_id)
INNER JOIN
    sakila.category as C
    ON (FC.category_id = C.category_id);
```

9. Utilizando o SELF JOIN, desenvolva uma _query_ que retorne a **duração do aluguel** e o **id do filme** para os filmes com a mesma duração. Retorne apenas o id do filme da instância um, e a duração do aluguel da instância dois. **Solução:**
```
SELECT T1.film_id, T2.rental_duration
FROM sakila.film AS T1, sakila.film AS T2
WHERE T1.length = T2.length;
```

# Bônus

**Exercício 10:** Utilizando o SELF JOIN, desenvolva uma _query_ que retorne o **título**, **duração** e **classificação** de todos os filmes que tem suas classificações iguais. **Solução:**
```
SELECT F1.title, F1.length, F2.rating
FROM sakila.film as F1, sakila.film as F2
WHERE (F1.rating = F2.rating);
```

**Exercício 11:** Utilizando o SELF JOIN, retorne o **endereço** e **id da cidade** para todos os endereços com o mesmo distrito. **Solução:**
```
SELECT A1.address, A1.city_id
FROM sakila.address AS A1, sakila.address AS A2
WHERE (A1.district = A2.district);
```

