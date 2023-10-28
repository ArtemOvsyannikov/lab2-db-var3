# Лабораторная работа №2. Вариант 3.

## Уровень 1

### Задание 1

![Alt text](https://ibb.co/RP5yf3S)
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
