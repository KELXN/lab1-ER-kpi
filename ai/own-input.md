Документ написаний без використання ШІ

Домен: Інтернет-магазин гаджетів «Gadget Zone»

1. Сутності та атрибути
 Client (Клієнт): id (string, PK), email (string), full_name (string), phone (string).
 Category (Категорія): id (string, PK), name (string).
 Product (Товар): id (string, PK), category_id (string, FK), name (string), price (decimal), stock_quantity (int).
 Order (Замовлення): id (string, PK), client_id (string, FK), status (string), total_amount (decimal), created_at (timestamp).
 OrderItem (Позиція замовлення): id (string, PK), order_id (string, FK), product_id (string, FK), quantity (int), unit_price (decimal).

2. Зв'язки між сутностями та кардинальність
 Client (1) до Order (0..N): Клієнт оформлює від 0..N замовлень; замовлення належить рівно одному клієнту.
 Category (1) до Product (0..N): Категорія містить від 0..N товарів; кожен товар належить рівно одній категорії.
 Order (1) до OrderItem (1..N): Замовлення містить щонайменше одну позицію; позиція належить одному замовленню.
 Product (1) до OrderItem (0..N): Товар може входити до 0..N позицій замовлень; позиція посилається на один товар.

3. Критерії прийняття
    1. Історія замовлень клієнта доступна з перевіркою статусу.
    2. Ціна в позиції замовлення (unit_price) фіксується на момент покупці і не залежить від майбутніх змін у каталозі (Product.price).
    3. Загальна сума замовлення (total_amount) зберігається для швидкого доступу та оптимізації звітів.