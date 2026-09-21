# UI/UX Design Specifications: Hardware Store POS

## 1. Design System & Theming
This project uses **Tailwind CSS** and **shadcn/ui** for rapid, accessible component development. The visual theme should reflect an industrial hardware store (clean, high-contrast, and functional).

*   **Color Palette (Tailwind):**
    *   **Primary:** `zinc-900` (Dark gray/black) for main buttons and active states.
    *   **Accent/Warning:** `amber-500` or `orange-500` for primary calls to action (e.g., "Checkout", "Pay Due"), reflecting a construction/hardware theme.
    *   **Success:** `emerald-600` for completed payments or delivered DOs.
    *   **Danger:** `red-600` for overdue debts, deleting items, or low stock alerts.
    *   **Background:** `slate-50` (Light gray) for the main application background to reduce eye strain, with `white` for cards and modals.
*   **Typography:** Use `Inter` or `Geist` (Next.js default fonts). Ensure large, readable numbers for pricing and quantities.
*   **Iconography:** Use `lucide-react` for all icons.

## 2. Global Layout Structure (App Shell)
*   **Sidebar Navigation:** A persistent left sidebar for desktop views (collapsible on tablet).
    *   Include a store logo at the top.
    *   Navigation links must be conditionally rendered based on RBAC (Admin, Cashier, Warehouse).
    *   Include a user profile/logout section at the bottom.
*   **Top App Bar:** 
    *   Display the current active branch/warehouse name.
    *   Show a real-time clock and network status indicator (Online/Offline).

## 3. Module-Specific UI Layouts

### A. Cashier POS Module (`/pos`)
**Layout:** 60/40 Split Screen (Left side for Products, Right side for Cart).
*   **Left Panel (Products):**
    *   Top sticky search bar (search by name, SKU, or barcode) and category filter chips.
    *   Grid layout (`grid-cols-3` or `grid-cols-4`) for product cards.
    *   **Product Card:** Show image (if available), Name, SKU, Base Price, and current stock level. Show a visual indicator (red text) if stock is low.
*   **Right Panel (Cart/Checkout):**
    *   List of selected items.
    *   **CRITICAL UX:** Each item row MUST have a dropdown to select the `unit` (e.g., switch from 'Kg' to 'Zak'). Changing this dropdown must instantly recalculate the line subtotal and required stock.
    *   Bottom sticky footer containing: Subtotal, Tax (if any), Grand Total, and a large "Checkout" button.
*   **Checkout Modal:**
    *   Step 1: Select Payment Method (Cash, QRIS, Tempo).
    *   Step 2 (If Tempo): Form to search/select `customer_id`, input `dp_amount` (Down Payment), and a date-picker for `due_date`.
    *   Large numeric keypad (optional, for touchscreens) to quickly input received cash.

### B. Warehouse Management Module (`/warehouse`)
**Layout:** Full-width Kanban Board for Delivery Orders (DO).
*   **Kanban Columns:** "Menunggu" (Pending) -> "Disiapkan" (Preparing) -> "Dikirim" (Shipping) -> "Selesai" (Delivered).
*   **DO Card:** Display DO Number, Cashier Name, Time elapsed since creation, and a short summary of heavy items (e.g., "50 Zak Semen").
*   **Interactivity:** Warehouse staff should be able to drag-and-drop cards between columns. Clicking a card opens a slide-out panel (Sheet component) showing the full list of items to prepare.

### C. Accounts Receivable / Piutang Module (`/receivables`)
**Layout:** Data Table View (Full width).
*   **Table Columns:** Customer Name, Phone, Credit Limit, Total Debt, Nearest Due Date, Action.
*   **Visual Indicators:**
    *   Use a red badge for "Overdue" (Jatuh Tempo).
    *   Use a yellow/amber badge for "Due in < 3 Days".
    *   Progress bar indicating Credit Limit usage (e.g., 80% used).
*   **Receive Payment Modal:** Triggered from the Action column. Shows outstanding invoices for that customer and an input field to record the payment amount.

## 4. UX & Interaction Rules
*   **Toast Notifications:** Use `sonner` or shadcn's toast to provide instant feedback for CRUD operations (e.g., "Transaction Successful", "Stock Deducted", "Error: Insufficient Stock").
*   **Loading States:** Use Skeleton loaders for the product grid and tables during data fetching. Avoid blocking full-page spinners.
*   **Confirmation Dialogs:** Always prompt an Alert Dialog before destructive actions or confirming a Tempo transaction.
*   **Responsive Design:** While POS interfaces are typically used on desktop/tablets, ensure the Warehouse Kanban board is usable on mobile devices (for staff walking around the warehouse).
*   
