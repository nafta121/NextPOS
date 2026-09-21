# AI Agent Execution Steps

You are an expert Full-Stack Engineer. Follow these steps sequentially to build the Hardware Store POS. Do not proceed to the next step until the current one is fully implemented and functional.

## Step 1: Project Initialization & Authentication
1. Initialize the Next.js (App Router) project with Tailwind CSS.
2. Install Supabase client and configure environment variables.
3. Build the Auth flow using Supabase Email/Password.
4. Implement Role-Based Access Control (RBAC) middleware to protect routes based on three roles: Admin, Cashier, Warehouse.

## Step 2: Database Scaffolding & Triggers
1. Generate the Supabase SQL migration script based on `ARCHITECTURE.md`.
2. Create the PostgreSQL Trigger for atomic inventory deduction when a transaction occurs (handling the conversion ratio).
3. Create the RPC function for inter-warehouse stock transfers.

## Step 3: Cashier POS Module
1. Build a responsive POS dashboard.
2. Implement a product grid with a search and barcode scan simulation.
3. Build the Cart component: Allow users to change the selling unit (e.g., from Kg to Zak) and dynamically update the price and required stock based on the `conversion_ratio`.
4. Build the Checkout Modal: Support Cash, QRIS, and 'Tempo'. If 'Tempo', enforce `customer_id` selection, Down Payment (DP) input, and a Due Date picker.

## Step 4: Warehouse & Delivery Order Module
1. Create a Kanban-style board for Warehouse staff to manage `delivery_orders`.
2. Use Supabase Realtime to automatically populate new DO tickets when the Cashier completes a transaction.
3. Add functionality to update DO status (Pending -> Preparing -> Shipping -> Delivered).

## Step 5: Accounts Receivable (AR) Module
1. Build a dashboard to display `customers` and their current debt.
2. Highlight debts that are past due or within 3 days of the due date.
3. Implement a 'Receive Payment' action to reduce a customer's `current_debt` when they pay their installments.
