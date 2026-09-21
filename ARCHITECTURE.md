# System Architecture & Database Schema

## 1. Database Schema (Supabase PostgreSQL)
The system must use a "Base Unit" approach for accurate inventory tracking. All backend stock calculations use the smallest unit, while the frontend handles conversions based on user selection.

*   `products`: id, sku, name, base_unit (string, e.g., 'kg', 'pcs'), category_id, created_at.
*   `product_units`: id, product_id, unit_name (e.g., 'Zak'), conversion_ratio (numeric, e.g., 50), price, barcode.
*   `warehouses`: id, name, type ('Main', 'Branch'), location.
*   `inventory`: id, product_id, warehouse_id, stock_base_unit (numeric).
*   `customers`: id, name, phone, credit_limit, current_debt.
*   `transactions`: id, invoice_no, customer_id (nullable), type ('Cash', 'Tempo'), status ('Paid', 'Partial', 'Unpaid'), total_amount, payment_method, dp_amount, due_date (nullable).
*   `transaction_items`: id, transaction_id, product_id, unit_id, qty, conversion_applied, subtotal.
*   `delivery_orders`: id, transaction_id, warehouse_id, do_number, status ('Pending', 'Preparing', 'Shipping', 'Delivered'), driver_name.

## 2. Critical Backend Logic (Supabase RPC & Triggers)
*   **Atomic Inventory Deduction:** Create a PostgreSQL Trigger on `transaction_items` INSERT. It must mathematically deduct `inventory.stock_base_unit` based on `transaction_items.qty` * `product_units.conversion_ratio`.
*   **Inter-Warehouse Transfer:** Use a Supabase RPC (Remote Procedure Call) to handle stock transfers between warehouses to ensure transactional integrity (commit both deduction and addition in a single SQL transaction).

## 3. Security (Row Level Security - RLS)
*   Enforce RLS on all tables based on user roles established in Supabase Auth metadata.
*   Cashiers can INSERT transactions but cannot DELETE them.
