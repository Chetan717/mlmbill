# Client PDF requirements — implementation checklist

Source: the user-supplied 3-page `software.pdf` (2026-10-28).

| PDF requirement | Where in demo |
|---|---|
| Franchise profile (name, logo, address, GST, phone, email) | **My Profile → Edit Profile**; shown in Invoice Print header |
| Dashboard total sale with custom date range | **Dashboard**, From/To inputs |
| Sale accordion: New Sale, Sale List, Quotation, Customer History | **Sale** expandable sidebar |
| Purchase accordion: New Order, Purchase List | **Purchase** expandable sidebar |
| Product accordion: Add Product, Delivery, Pending, Stock, Low Stock, Return, Leakage | **Product** expandable sidebar |
| Payment accordion: Customer Dues, Cash & Bank, Daily Cash Closing | **Payment** expandable sidebar |
| Customer entry / alphabetical suggestions, auto-fill | **Sale → New Sale** modal, name field |
| Auto date and sequential invoice number | **Sale → New Sale** modal; calculated from existing invoice IDs |
| Combined cash and bank/online payment, duplicate UTR warning | **Sale → New Sale** and **Payment → Customer Dues → Receive Dues** |
| Invoice list date range, customer/mobile search, totals | **Sale → Sale List** |
| Print relevant point type per product | Invoice Print / New Sale item lines |
| One point type per product, SP/BV/PV/etc | **Product → Add Product** (SP/BV/PV/None) |
| Product opening quantity | **Product → Add Product** |
| Stock ₹ valuation, product-wise and overall | **Product → Stock** |
| Order without stock receipt; Purchase List on receiving | **Purchase → New Order / Purchase List** |
| Purchase List date filter and totals | **Purchase → Purchase List** |

## Previous approved scope retained

- Stock deducts **only on confirmed delivery** (not invoice creation).
- Pending customer product delivery searched by customer/mobile/product/invoice.
- Only **good received** purchase items increase stock; leakage creates separate company claim.
- Cash/bank balances, dues history, customer ledger, refunds, staff demo, audit, stock adjustment, low stock, unused invoice points, WhatsApp preview and SaaS admin presentation.

## Implementation status

This is a **frontend-only interactive demo**: data is in localStorage and editable by the browser. Production-grade authentication, true company tenant isolation, payments, tax compliance, file storage and WhatsApp integration **are not implemented**. All amounts are sample data. Do not use for actual financial operations.

## Checks performed

- JSX/JS parsed with TypeScript compiler: PASS.
- JSX transpilation: PASS.
- Mock-React runtime smoke checks for Dashboard, accordion, New Sale, Sale List, Profile, Purchase List, Stock valuation and Customer Dues form: PASS.
- Actual `npm run build`: **not run to completion here**, because the execution environment cannot resolve `registry.npmjs.org` to install dependencies. Vercel has network access and will install dependencies using `vercel.json`.
