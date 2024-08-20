**1. Создание базы данных и выбор её для использования:**

```sql
CREATE DATABASE Tourism;
USE Tourism;
```

- **CREATE DATABASE Tourism;** — команда создает новую базу данных с названием "Tourism".
- **USE Tourism;** — эта команда выбирает базу данных "Tourism" для использования в последующих запросах.

**2. Таблица Services:**

```sql
CREATE TABLE Services (
    service_id INT PRIMARY KEY AUTO_INCREMENT,
    service_name VARCHAR(255) NOT NULL,
    description TEXT,
    price DECIMAL(10, 2) NOT NULL
);
```

- **service_id INT PRIMARY KEY AUTO_INCREMENT;** — создается первичный ключ `service_id`, который является уникальным идентификатором каждой записи в таблице. `AUTO_INCREMENT` автоматически увеличивает значение `service_id` при добавлении новой записи.
- **service_name VARCHAR(255) NOT NULL;** — поле для хранения названия услуги. Тип данных `VARCHAR(255)` означает, что максимальная длина строки — 255 символов. `NOT NULL` указывает, что это поле обязательно должно быть заполнено.
- **description TEXT;** — текстовое поле для хранения описания услуги. Тип `TEXT` позволяет хранить длинный текст.
- **price DECIMAL(10, 2) NOT NULL;** — поле для хранения стоимости услуги. Тип `DECIMAL(10, 2)` означает, что число может содержать до 10 цифр, из которых 2 будут после запятой. `NOT NULL` указывает на обязательное заполнение.

**3. Таблица Clients:**

```sql
CREATE TABLE Clients (
    client_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    phone VARCHAR(20)
);
```

- **client_id INT PRIMARY KEY AUTO_INCREMENT;** — создается первичный ключ `client_id` с автоинкрементом, обеспечивающий уникальность каждого клиента.
- **first_name VARCHAR(100) NOT NULL;** — поле для хранения имени клиента. Длина имени ограничена 100 символами, поле обязательно для заполнения.
- **last_name VARCHAR(100) NOT NULL;** — поле для хранения фамилии клиента, аналогично имени.
- **email VARCHAR(255) UNIQUE NOT NULL;** — поле для хранения email-адреса клиента. `UNIQUE` обеспечивает уникальность значений в этом поле, `NOT NULL` указывает на обязательное заполнение.
- **phone VARCHAR(20);** — поле для хранения номера телефона клиента. Это поле необязательно для заполнения.

**4. Таблица Operators:**

```sql
CREATE TABLE Operators (
    operator_id INT PRIMARY KEY AUTO_INCREMENT,
    operator_name VARCHAR(255) NOT NULL,
    contact_number VARCHAR(20),
    email VARCHAR(255) UNIQUE NOT NULL
);
```

- **operator_id INT PRIMARY KEY AUTO_INCREMENT;** — первичный ключ `operator_id` с автоинкрементом, идентифицирующий каждого туроператора.
- **operator_name VARCHAR(255) NOT NULL;** — поле для хранения названия оператора, обязательное для заполнения.
- **contact_number VARCHAR(20);** — поле для хранения контактного номера оператора, необязательное для заполнения.
- **email VARCHAR(255) UNIQUE NOT NULL;** — поле для хранения email-адреса оператора, должно быть уникальным и обязательным для заполнения.

**5. Таблица Tours:**

```sql
CREATE TABLE Tours (
    tour_id INT PRIMARY KEY AUTO_INCREMENT,
    tour_name VARCHAR(255) NOT NULL,
    destination VARCHAR(255) NOT NULL,
    duration_days INT NOT NULL,
    operator_id INT,
    FOREIGN KEY (operator_id) REFERENCES Operators(operator_id)
);
```

- **tour_id INT PRIMARY KEY AUTO_INCREMENT;** — первичный ключ `tour_id`, уникальный идентификатор для каждого тура.
- **tour_name VARCHAR(255) NOT NULL;** — поле для хранения названия тура, обязательное для заполнения.
- **destination VARCHAR(255) NOT NULL;** — поле для хранения пункта назначения тура, обязательное для заполнения.
- **duration_days INT NOT NULL;** — поле для хранения длительности тура в днях, обязательное для заполнения.
- **operator_id INT;** — внешний ключ, который ссылается на таблицу `Operators` и указывает, какой оператор организует этот тур.
- **FOREIGN KEY (operator_id) REFERENCES Operators(operator_id);** — эта строка создает связь между `Tours` и `Operators`, где `operator_id` в таблице `Tours` ссылается на `operator_id` в таблице `Operators`.

**6. Таблица Orders (переменная информация):**

```sql
CREATE TABLE Orders (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    client_id INT,
    tour_id INT,
    service_id INT,
    order_date DATE NOT NULL,
    total_price DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (client_id) REFERENCES Clients(client_id),
    FOREIGN KEY (tour_id) REFERENCES Tours(tour_id),
    FOREIGN KEY (service_id) REFERENCES Services(service_id)
);
```

- **order_id INT PRIMARY KEY AUTO_INCREMENT;** — первичный ключ `order_id`, уникальный идентификатор для каждого заказа.
- **client_id INT;** — внешний ключ, ссылающийся на `client_id` в таблице `Clients`, указывает, какой клиент сделал заказ.
- **tour_id INT;** — внешний ключ, ссылающийся на `tour_id` в таблице `Tours`, указывает на заказанный тур.
- **service_id INT;** — внешний ключ, ссылающийся на `service_id` в таблице `Services`, указывает на услуги, включенные в заказ.
- **order_date DATE NOT NULL;** — поле для хранения даты заказа, обязательное для заполнения.
- **total_price DECIMAL(10, 2) NOT NULL;** — поле для хранения общей стоимости заказа, обязательное для заполнения.
- **FOREIGN KEY (client_id) REFERENCES Clients(client_id);** — создает связь с таблицей `Clients`.
- **FOREIGN KEY (tour_id) REFERENCES Tours(tour_id);** — создает связь с таблицей `Tours`.
- **FOREIGN KEY (service_id) REFERENCES Services(service_id);** — создает связь с таблицей `Services`.

---

В результате выполнения данного кода, создается база данных "Tourism" с пятью таблицами: `Services`, `Clients`, `Operators`, `Tours`, и `Orders`. Таблицы `Services`, `Clients`, `Operators`, и `Tours` являются справочниками и содержат фиксированную информацию, а таблица `Orders` хранит переменную информацию о заказах, ссылаясь на другие таблицы через внешние ключи.
