# Product Requirements Document (PRD): Hardware Store POS 

## 1. Project Overview
A modern Point of Sale (POS) and inventory management system designed specifically for hardware stores (Toko Bangunan). It handles complex operations such as multi-unit conversions (e.g., Sack to Kg), contractor credit management (Accounts Receivable), multi-warehouse tracking, and Delivery Order (Surat Jalan) workflows.

## 2. Tech Stack
*   **Frontend:** Next.js (App Router), React, Tailwind CSS, shadcn/ui (for UI components).
*   **Backend & Database:** Supabase (PostgreSQL, Auth, RLS, Realtime, RPC/Triggers).
*   **Deployment:** Vercel.

## 3. User Roles & Access Control
*   **Admin (Owner):** Full access to all modules, financial reports, master data, and inter-warehouse transfers.
*   **Cashier (Kasir):** Access to POS interface, product search, cart management, and transaction checkout (Cash, QRIS, Credit/Tempo).
*   **Warehouse Staff (Gudang):** Access to Delivery Orders (Surat Jalan) board, stock monitoring, and preparing items for shipping.

## 4. Core Features
*   **Multi-Unit Conversion:** Automatically calculate prices and deduct base inventory when selling in different units (e.g., selling 1 Zak of cement deducts 50 Kg from base stock).
*   **Accounts Receivable (Piutang & Tempo):** Manage contractor credit limits, track down payments (DP), and monitor due dates.
*   **Multi-Warehouse Management:** Track real-time inventory across the Main Store and Branch Warehouses.
*   **Delivery Order (DO) Workflow:** Cashier transactions automatically generate DO tickets for the warehouse team to fulfill.
