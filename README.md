# MLM Franchise Billing SaaS — React Client Demo

A single React + Vite app for demonstrating the **approved** MLM Franchise SaaS feature scope to clients. **No backend, no API calls, no server database, no WhatsApp connection.** Demo data is preloaded and updates are stored in the browser's localStorage.

## Run

1. Install Node.js 20.19+ or 22.12+.
2. In this folder run `npm install`.
3. Run `npm run dev`.
4. Open the localhost URL displayed by Vite (usually http://localhost:5173).
5. To generate a static client presentation site, run `npm run build` and host the `dist/` folder on any static host.

## Included demonstration screens

- Updated dashboard: Cash in Hand, Bank Balance, New Sale, New Sale Payment, Dues Collection, Total Payment Received, Customer Dues, Pending Product Delivery, Leakage Claims, Low Stock, illustrative chart, quick actions. No New Customers / Recent Invoices / Recent Payments widgets.
- Customers & ledger, sale invoices, partial payments, cash/bank, UTR uniqueness check, invoice print, dues receipt by collection date.
- Invoice-wise and product-wise pending deliveries, searchable customer/mobile/invoice/product, partial/full delivery, stock deduction **only on confirmed delivery**.
- Company orders (no stock increase on order), good/leakage split on receipt, company invoice, leakage replacement, leakage never enters physical stock.
- Cash-to-bank transfer, SP/BV/PV, unused invoice points, staff/role preview, daily cash closing, returns/refunds/exchange record, audit, stock adjustments, low-stock alerts, reports, multi-company/franchise admin preview, WhatsApp message preview.

## Honest demo limitations

- Frontend-only **client demonstration**, not a secure accounting system. Browser data can be edited, reset, or cleared. No auth, real staff permissions, or tenant isolation.
- SaaS franchise selector previews franchise identity; demo records are shared across selections.
- WhatsApp connection is a mock preview only. Official QR / WhatsApp Business API requires external infrastructure.
- File attachments are represented by reference text; there is no real file upload/storage.
- Charts use illustrative demo data. Other screens update from local demo state.
- Exchange is a return record; separate replacement sale flow is not automated.
- Refund, cash and stock rules are simplified to illustrate behavior; do not use for live transactions.
- No real API requests are made. Dependencies are downloaded once at `npm install`.

## Reset

Use **Reset Demo Data** at the bottom of the left navigation. You can also clear this site's localStorage.
