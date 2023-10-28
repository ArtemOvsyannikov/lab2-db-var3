# Лабораторная работа №2. Вариант 3.

## Уровень 1

### Задание 1

<image src="https://camo.githubusercontent.com/97222b764228d3e897bdea3c94ea7be4dfc485cb98cc3c7a000e328e19f70356/68747470733a2f2f692e6962622e636f2f63746d4c3036762f312e706e67" alt="Задание 1">
	
```
CREATE TABLE customer (
    id INT NOT NULL PRIMARY KEY, -- целочисленный идентификатор, обязательно должен быть
    lastname VARCHAR(50) NOT NULL, -- фамилия заказчика обычной строкой, обязательно должна быть, 50 символов на всякий случай
    neighborhood VARCHAR(50) NOT NULL, -- район, обычная строка, обязательно должен быть, 50 символов на всякий случай 
    discount INT NOT NULL CHECK (discount >= 0 AND discount <= 100)  -- скидка, целое число процентов, обязательно должна быть, проверка на адекватность
);

CREATE TABLE item_rental (
	id INT NOT NULL PRIMARY KEY, -- целочисленный идентификатор, обязательно должен быть
	number VARCHAR(10) NOT NULL, -- номер в виде числа, обязательно должен быть
	location VARCHAR(25) NOT NULL, -- аналогично с районом в предыдущей таблице, обязательно должен быть
	commission INT NOT NULL CHECK (commission >= 0 AND commission <= 100) -- комиссионные, по аналогии со скидкой, просто целое число, обязательно должно быть
);

CREATE TABLE items (
    id INT NOT NULL PRIMARY KEY, -- целочисленный идентификатор, обязательно должен быть
    name VARCHAR(100) NOT NULL, -- название вещи, строка на 100 символов (чтоб наверняка влезло) 
    warehouse VARCHAR(25) NOT NULL, -- аналогично с локацией в предыдущей таблице, обязательно должен быть
    quantity INT NOT NULL, -- целочисленное количество данной вещицы, обязательно должен быть
    rental_price_per_week INT NOT NULL -- целочисленная цена проката за неделю, обязательно должен быть 
);


CREATE TABLE rental_list (
	id INT NOT NULL PRIMARY KEY, -- номер проката выполняет функцию целочисленного идентификатора, обязательно должен быть
	customer INT NOT NULL REFERENCES customer(id), -- связываем айди заказчика с айдишником в таблице заказчиков, обязательно должен быть
	date VARCHAR(15) NOT NULL, -- так как дан только месяц словом, то юзаем строку вместо даты, обязательно должен быть
	item_rental INT NOT NULL REFERENCES item_rental(id), -- связываем айди пункта проката с айдишником в соотв. таблице, обязательно должен быть
	item INT NOT NULL REFERENCES items(id), -- связываем айди вещи с айдишником в соотв. таблице, обязательно должен быть
	rental_term INT NOT NULL, -- целочисленный срок проката (кол-во недель), обязательно должен быть
	amount INT NOT NULL -- итоговая сумма, целое число, , обязательно должен быть
);
```

### Задание 2

<a href="https://ibb.co/PM4kYc7"><img src="https://i.ibb.co/nBfp07H/2.png" alt="2" border="0"></a>
	
```
INSERT INTO customer (id, lastname, neighborhood, discount) VALUES
	(001, 'Жалнин', 'Приокский', 2),
	(002, 'Семенов', 'Советский', 6),
	(003, 'Кожаков', 'Ленинский', 0),
	(004, 'Шерстнев', 'Автозаводский', 0),
	(005, 'Козлов', 'Нижегородский', 4);

INSERT INTO item_rental (id, number, location, commission) VALUES
	(001, 'N23', 'Нижегородский', 4),
	(002, 'N16', 'Советский', 5),
	(003, 'N8', 'Сормовский', 7),
	(004, 'N21', 'Приокский', 3),
	(005, 'N12', 'Нижегородский', 2),
	(006, 'N6', 'Канавинский', 5);

INSERT INTO items (id, name, warehouse, quantity, rental_price_per_week) VALUES
	(001, 'Телевизор', 'Нижегородский', 7, 10000),
	(002, 'Часы напольные', 'Советский', 6, 5000),
	(003, 'Радиоприемник', 'Нижегородский', 10, 7000),
	(004, 'Часы настенные', 'Приокский', 20, 3000),
	(005, 'Холодильник', 'Сормовский', 6, 12000),
	(006, 'Утюг', 'Нижегородский', 30, 2000),
	(007, 'Весы детские', 'Нижегородский', 15, 1500);

INSERT INTO rental_list (id, customer, date, item_rental, item ,rental_term ,amount) VALUES
	 (10005, 002 ,'Январь', 003, 003, 4, 28000),
	 (10006, 003 ,'Январь', 003, 007, 1, 1500),
	 (10007, 004 ,'Январь', 002, 006, 8, 16000),
	 (10008, 003 ,'Февраль', 002, 005, 4, 48000),
	 (10009, 004 ,'Февраль', 001, 001, 4, 40000),
	 (10010, 005 ,'Март', 003, 006, 4, 8000),
	 (10011, 005 ,'Март', 006, 003, 8, 56000),
	 (10012, 001 ,'Апрель', 003, 003, 8, 56000),
	 (10013, 004 ,'Апрель', 004, 002, 2, 10000),
	 (10014, 002 ,'Май', 005, 007, 2, 3000),
	 (10015, 004 ,'Май', 006, 004, 1, 3000),
	 (10016, 004 ,'Май', 002, 001, 11, 110000), 
	 (10017, 003, 'Июнь', 001, 001, 1, 10000), 
	 (10018, 005, 'Июль', 001, 007, 1, 1500), 
	 (10019, 003, 'Август', 003, 002, 4 , 20000), 
	 (10020, 004, 'Август', 005, 002, 4 , 20000),
	 (10021, 001, 'Август', 003, 001, 2 , 20000);
```

### Задание 3

<a href="https://ibb.co/GHHQhqf"><img src="https://i.ibb.co/Bnn219H/3.png" alt="3" border="0"></a>
	
```
SELECT * FROM customer;
SELECT * FROM item_rental;
SELECT * FROM items;
SELECT * FROM rental_list;
```

### Задание 4

<a href="https://imgbb.com/"><img src="https://i.ibb.co/ns1f5x9/4.png" alt="4" border="0"></a>

а)	
```
SELECT DISTINCT lastname, discount FROM customer;
```

b)	
```
SELECT DISTINCT neighborhood FROM customer;
```

c)	
```
SELECT DISTINCT number, location FROM item_rental;
```

### Задание 5

<a href="https://ibb.co/mFshtqM"><img src="https://i.ibb.co/G3wCk2b/5.png" alt="5" border="0"></a>
	
а)	
```
SELECT id, lastname FROM customer
WHERE neighborhood = 'Приокский' OR neighborhood = 'Сормовский' OR lastname LIKE '%ин';
```

b)	
```
SELECT id, date, rental_term, amount FROM rental_list
WHERE amount > 2000
ORDER BY amount ASC, rental_term ASC;
```

c)	
```
SELECT name, warehouse FROM items
WHERE quantity >= 7;
```

### Задание 6

<a href="https://ibb.co/BttrXyR"><img src="https://i.ibb.co/c11CG6d/6.png" alt="6" border="0"></a>
	
а)	
```
SELECT c.lastname, ir.number, rl.date, rl.id 
FROM rental_list rl, customer c, item_rental ir 
WHERE rl.customer = c.id AND rl.item_rental = ir.id
ORDER BY c.lastname ASC, ir.number ASC;
```

b)	
```
SELECT ir.number, rl.date, i.name, rl.amount 
FROM rental_list rl, item_rental ir, items i 
WHERE rl.item_rental = ir.id AND rl.item = i.id;
```

### Задание 7

<a href="https://ibb.co/FDqFP0c"><img src="https://i.ibb.co/bKRkf2Y/7.png" alt="7" border="0"></a>
	
а)	
```
SELECT DISTINCT ir.number FROM item_rental ir
JOIN rental_list rl ON ir.id = rl.item_rental
JOIN items i ON rl.item = i.id
JOIN customer c ON rl.customer = c.id
WHERE i.name = 'Утюг' OR ir.location = c.neighborhood;
```

b)	
```
SELECT DISTINCT c.lastname, c.neighborhood, ir.number FROM rental_list rl
JOIN customer c ON rl.customer = c.id
JOIN item_rental ir ON rl.item_rental = ir.id
JOIN items i ON rl.item = i.id
WHERE i.rental_price_per_week > 8000 AND rl.date != 'Январь'
ORDER BY ir.number;
```

c)	
```
SELECT i.name, i.rental_price_per_week FROM rental_list rl
JOIN customer c ON rl.customer = c.id
JOIN item_rental ir ON rl.item_rental = ir.id
JOIN items i ON rl.item = i.id
WHERE c.lastname = 'Кожаков' AND ir.location != c.neighborhood;
```

d)	
```
SELECT i.name, i.quantity FROM rental_list rl
JOIN items i ON rl.item = i.id
GROUP BY i.name, i.quantity
HAVING COUNT(rl.item_rental) > 1;
```

### Задание 8

<a href="https://ibb.co/K7p8Kbw"><img src="https://i.ibb.co/6b7qXrB/8.png" alt="8" border="0"></a>
	
```
UPDATE rental_list SET amount = amount - (amount * customer.discount / 100)
FROM customer 
WHERE rental_list.customer = customer.id;

SELECT * FROM rental_list;
```

### Задание 9

<a href="https://ibb.co/yhz5s9z"><img src="https://i.ibb.co/q0H91SH/9.png" alt="9" border="0"></a>
	
```
ALTER TABLE rental_list ADD COLUMN commission_amount INT;

UPDATE rental_list
SET commission_amount = amount * (SELECT commission FROM item_rental WHERE rental_list.item_rental = item_rental.id) / 100;

SELECT * FROM rental_list;
```

### Задание 10

<a href="https://ibb.co/Q9h0t72"><img src="https://i.ibb.co/kKzZvVR/10.png" alt="10" border="0"></a>
	
а)	
```
SELECT i.name FROM items i
WHERE i.id IN (
    SELECT r_l.item FROM rental_list r_l
    JOIN customer c ON r_l.customer = c.id
    WHERE c.discount > 2
);
```

b)	
```
SELECT i.name FROM items i
WHERE i.id IN (
    SELECT r_l.item FROM rental_list r_l
    JOIN customer c ON r_l.customer = c.id
    JOIN item_rental i_r ON r_l.item_rental = i_r.id
    WHERE c.neighborhood = i_r.location
);
```

c) (7b)	
```
SELECT DISTINCT c.lastname, c.neighborhood, ir.number FROM rental_list rl
JOIN customer c ON rl.customer = c.id
JOIN item_rental ir ON rl.item_rental = ir.id
JOIN items i ON rl.item = i.id
WHERE i.rental_price_per_week > 8000 AND rl.date NOT IN('Январь')
ORDER BY ir.number;
```

c) (7c)
```
SELECT DISTINCT i.name, i.rental_price_per_week FROM rental_list rl
JOIN customer c ON rl.customer = c.id
JOIN item_rental ir ON rl.item_rental = ir.id
JOIN items i ON rl.item = i.id
WHERE c.lastname = 'Кожаков' AND ir.location NOT IN (
	SELECT neighborhood FROM customer 
	WHERE lastname = 'Кожаков'
);
```

### Задание 11

<a href="https://ibb.co/SQR35Pb"><img src="https://i.ibb.co/Q8rKpfL/11.png" alt="11" border="0"></a>
	
а)	
```
SELECT DISTINCT i.name FROM rental_list r_l
JOIN items i ON r_l.item = i.id
WHERE date IN ('Июнь', 'Июль', 'Август') 
AND r_l.rental_term >= ALL (
  SELECT rental_term FROM rental_list
  WHERE date IN ('Июнь', 'Июль', 'Август')
)
```

b)	
```
SELECT ir.number FROM item_rental ir 
WHERE ir.id = ALL (
    SELECT rl.item_rental FROM rental_list rl 
    JOIN items i ON rl.item = i.id 
    WHERE i.rental_price_per_week = (SELECT MAX(rental_price_per_week) FROM items)
);
```

c)	
```
SELECT c.lastname FROM customer c
WHERE c.discount = ANY (
    SELECT c2.discount FROM customer c2
    JOIN rental_list r ON c2.id = r.customer
    WHERE r.item = 3
);
```

d)	
```
SELECT ir.number FROM item_rental ir
JOIN rental_list rl ON ir.id = rl.item_rental
JOIN items i ON rl.item = i.id
WHERE i.name = 'Утюг' 
OR ir.location = ANY (
	SELECT neighborhood FROM customer c
	WHERE c.id = rl.customer
);
```

### Задание 12

<a href="https://ibb.co/0rwSxDj"><img src="https://i.ibb.co/x640NCS/12.png" alt="12" border="0"></a>
	
```
SELECT neighborhood FROM customer 
UNION
SELECT location FROM item_rental;
```

### Задание 13

<a href="https://ibb.co/yPF87cg"><img src="https://i.ibb.co/c3hNVS2/13.png" alt="13" border="0"></a>
	
а)	
```
SELECT i.name, i.rental_price_per_week FROM items i
WHERE EXISTS (
    SELECT * FROM rental_list rl
    WHERE rl.item = i.id AND rl.date NOT IN ('Ноябрь', 'Декабрь')
)
ORDER BY i.rental_price_per_week DESC LIMIT 2;
```

b)	
```
SELECT ir.number FROM item_rental ir
WHERE NOT EXISTS (
    SELECT * FROM items i
    WHERE NOT EXISTS (
        SELECT * FROM customer c
        JOIN rental_list rl ON rl.customer = c.id AND rl.item = i.id
        WHERE c.neighborhood = 'Нижегородский' AND rl.item_rental = ir.id
    )
);
```

c)	
```
SELECT lastname FROM customer c
WHERE NOT EXISTS (
    SELECT * FROM rental_list r_l, items i, item_rental i_r 
    WHERE r_l.customer = c.id 
    AND r_l.item = i.id AND r_l.item_rental = i_r.id 
    AND i.rental_price_per_week < 5000 AND c.neighborhood != i_r.location
);
```

d)	
```
SELECT c.lastname FROM customer c
WHERE NOT EXISTS (
    SELECT * FROM item_rental ir
    WHERE ir.commission < 5 AND NOT EXISTS (
        SELECT * FROM rental_list rl
        WHERE rl.customer = c.id AND rl.item_rental = ir.id
    )
);
```

### Задание 14

<a href="https://ibb.co/qkXdwF6"><img src="https://i.ibb.co/XSNbTkH/14.png" alt="14" border="0"></a>
	
а)	
```
SELECT AVG(rental_term) 
FROM rental_list 
JOIN item_rental ON rental_list.item_rental = item_rental.id 
WHERE item_rental.location = 'Советский';
```

b)	
```
SELECT c.lastname, c.discount FROM customer c
WHERE c.discount = (
    SELECT MIN(c.discount) FROM rental_list r_l
    JOIN customer c ON r_l.customer = c.id
    JOIN item_rental i_r ON r_l.item_rental = i_r.id
    WHERE i_r.number = 'N8'
)
GROUP BY c.lastname, c.discount LIMIT 1;
```

c)	
```
SELECT r_l.* FROM rental_list r_l
JOIN item_rental i_r ON r_l.item_rental = i_r.id
WHERE r_l.amount > (
    SELECT AVG(r_l.amount) FROM rental_list r_l
    JOIN item_rental sub_i_r ON r_l.item_rental = sub_i_r.id
    WHERE sub_i_r.location = i_r.location
);
```

d)	
```
SELECT c.lastname, COUNT(*) FROM rental_list rl
JOIN customer c ON rl.customer = c.id
WHERE c.lastname = 'Семенов'
GROUP BY c.lastname;
```

### Задание 15

<a href="https://ibb.co/thy0jdx"><img src="https://i.ibb.co/VNXFnKQ/15.png" alt="15" border="0"></a>
	
а)	
```
SELECT i.name, SUM(r.amount) FROM rental_list r
JOIN items i ON r.item = i.id
GROUP BY i.name;
```

b)	
```
SELECT item, AVG(rental_term) FROM rental_list
WHERE date IN ('Октябрь', 'Ноябрь', 'Декабрь')
GROUP BY item;
```

c)	
```
SELECT c.lastname, COUNT(r.item) FROM rental_list r
JOIN customer c ON r.customer = c.id
WHERE r.item_rental IN (
	SELECT id FROM item_rental 
	WHERE location = 'Советский'
)
GROUP BY c.lastname;
```

d)	
```
SELECT ri.number, i.name, SUM(r.amount) FROM rental_list r
JOIN items i ON r.item = i.id
JOIN item_rental ri ON r.item_rental = ri.id
GROUP BY ri.number, i.name;
```
