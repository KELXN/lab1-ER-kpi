# Специфікація вимог та модель даних (Gadget Zone)

## 1. Намір
Створення логічної моделі даних для інтернет-магазину електроніки та ґаджетів з метою забезпечення підтримки каталогу, обліку клієнтів, обробки замовлень та коректного зв'язку багато-до-багатьох для товарів у замовленні без надлишковості.

## 2. Сутності та атрибути
- **Client**: `client_id` (PK, string), `full_name` (string), `email` (string), `phone` (string)
- **Category**: `category_id` (PK, string), `name` (string), `description` (string)
- **Product**: `product_id` (PK, string), `category_id` (FK, string), `title` (string), `price` (decimal), `stock_quantity` (integer)
- **Order**: `order_id` (PK, string), `client_id` (FK, string), `order_date` (timestamp), `status` (string), `total_amount` (decimal)
- **OrderItem**: `order_id` (PK/FK, string), `product_id` (PK/FK, string), `quantity` (integer), `unit_price` (decimal)

## 3. Критерії прийняття
1. Усі ідентифікатори типізовані однаково (`string` / UUID).
2. Зв'язок між замовленнями та товарами декомпозовано через асоціативну сутність `OrderItem` (3NF), що містить атрибути `quantity` та `unit_price`.
3. Усі зовнішні ключі відповідають первинним ключам батьківських сутностей.