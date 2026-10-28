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

## `softwar2e.pdf` update acceptance checklist

- [x] Invoice Date (left) / Invoice No (right)
- [x] Editable quantity after product added to New Sale
- [x] Qty / Price / Point / Amount footer in cart and invoice details
- [x] Per-product Delivered/Paid vs Product Dues quantity on invoice
- [x] Point Used date and time
- [x] Quotation with customer details, multiple lines, Convert to Sale
- [x] New Order list / button, multiple products, editable qty, company contact
- [x] New Order auto order number/date and View Invoice
- [x] Purchase List only received receipts, auto Purchase Invoice on Receive, View Invoice
- [x] SKU removed from new Product form
- [x] Unused Points search by invoice/customer + date filter
- [x] Invoice fixed in Mark Points Used and Dues Payment dialogs
- [x] Billed column removed from product delivery views
- [x] Refund/Return invoice search, per-product selection + all return, refund amounts from Cash/Bank
- [x] Leakage replacement products grouped under Company Invoice with per-product qty
- [x] Vercel Vite executable-permission workaround and clean-install config

**Demo scope:** These are interactive frontend demonstrations, **not real accounting transactions**. Replacement delivery for Exchange remains a separate demo follow-up, not an automated transaction. Vite production build was not verified in the current environment due npm registry timeout.
