# MLM Franchise Billing SaaS — React Client Demo (PDF Updates + Vercel Fix)

**Purpose:** Show the client how the approved MLM Franchise SaaS works. This is a **frontend-only React + Vite demonstration** with sample data, saved in the browser's `localStorage`. There are **no external APIs, backend services, database, production authentication, or real WhatsApp integration**.

## Run locally

Requires Node.js 20.19+ or Node.js 22.12+.

```bash
npm install
npm run dev
```

Open the local URL displayed in your terminal.

## Deploy to Vercel

1. Upload the **project files** to GitHub, **not** `node_modules/` or `dist/`.
2. Use Framework Preset **Vite**, Root Directory `./`, Install Command `rm -rf node_modules && npm install --include=dev`, Build Command `npm run build` (executes Vite via Node to avoid UNIX executable permission issues), Output Directory `dist`.
3. Redeploy without the previous build cache if the old deployment copied Windows `node_modules` into the repository.

**To remove previously tracked `node_modules` from the existing Git repository:**

```bash
git rm -r --cached node_modules
# If Git says "pathspec ... did not match", it's already untracked.
git add .
git commit -m "Update SaaS demo and fix Vercel dependencies"
git push origin main
```

The `.gitignore` prevents future dependency/build folder commits. `vercel.json` provides stable Vite settings and SPA route fallback.

## Changes implemented from `software.pdf`

- **My Profile**: franchise name, logo (local browser demo), address, GST number, mobile number, email; appears at the top of the printed invoice.
- **Dashboard**: selectable custom date range with Total Sale, New Sale Payment, Dues Collection Payment and Total Payment; Cash & Bank balances remain; no Recent Payments, Recent Invoices or New Customer widget.
- **Accordion sidebar**: Sale (New Sale, Sale List, Quotation, Customer History), Purchase (New Order, Purchase List), Product (Add Product, Product Delivery, Pending Product Delivery, Stock, Low Stock Alert, Return/Refund/Exchange, Leakage Claims), Payment (Customer Dues, Cash & Bank, Daily Cash Closing). Click again to collapse.
- **New Sale**: name entry with matching customer suggestions and full autofill, mobile and address, auto invoice date and sequential invoice number; new customers are saved for future use.
- **Split payments**: Cash + Online/Bank amounts for New Sale and Customer Dues, mandatory UTR if online amount > 0, duplicate UTR rejection across **all** sale/dues payments with the existing invoice number shown.
- **Sale List**: filter by customer name/mobile/invoice and custom date range; total invoice count, sale amount, payments and remaining outstanding.
- **Quotation**: basic quotation creation & history with date filter; no effect on stock or collections.
- **Product**: choose **exactly one** point type per product (SP, BV or PV, or None) and one point value, add opening physical quantity. Invoice points show each product's applicable type only.
- **Stock**: current physical quantity, purchase-price stock valuation per product and overall totals.
- **Company Purchase**: orders stay in New Order until products received; received/partial receipts in Purchase List, date filter and totals. Stock goes up **only for good received products**, while leakage stays in separate claims.
- **Product Delivery**: invoice creation never deducts stock; confirmed product-wise delivery does. Pending delivery is searchable by customer/mobile/product/invoice and shows current stock availability.
- **Existing approved client demo**: customer history/ledger, dues, cash-bank transfer, leakage claims/replacement, returns, cash closing, audit, stock adjustment, low-stock alerts, unused points, staff demo, WhatsApp preview and SaaS admin preview.

## Demo limitations

This is **not production accounting software**. Data lives only in one browser (can be cleared/reset); franchise switching is illustrative, not tenant isolation. Receipt references and WhatsApp are previews; no real uploads, messaging or billing API. Demo roles are not a security boundary. Cash, taxes and financial rules need production-grade backend validation before actual business use.

**Reset data:** Use “Reset Demo Data” in the sidebar. Existing browser data from an earlier demo version may need to be reset for the updated sample point types/profiles to appear.

## Vercel `vite: Permission denied` mitigation

The Vercel installation step force-removes any `node_modules` checked into the repository and installs Linux-compatible packages again. The build script calls `node ./node_modules/vite/bin/vite.js build` instead of directly executing the `vite` shim. This specifically addresses the earlier error `node_modules/.bin/vite: Permission denied` (exit 126). **Still delete tracked `node_modules` from GitHub** with the command above; `.gitignore` alone does not remove already tracked files.

## New changes from `softwar2e.pdf` (28 Oct 2026)

All updates below are part of the **same frontend-only React SaaS client demo**; no real API was added.

- **New Sale invoice header:** invoice date on the left and running invoice number on the right, labeled `Invoice No.`. After adding a product, edit its quantity directly in the cart. A footer totals quantity, the unit-price column, points by type, and line amounts.
- **Invoice details / print:** totals beneath Qty / Price / Point / Amount; product delivery shows `Paid / Delivered` or `Dues N pcs`; point-used records Distributor ID and India-local date/time.
- **Quotation:** Customer Name, Mobile, Address and product lines with editable quantities. `Convert to Sale` prefills the billing form, then creating the sale generates a new serial invoice number. The quotation by itself never affects physical stock or funds.
- **Company New Order:** order list and button; order date/serial; company name/mobile/email/address; multiple product lines and editable quantities. Creating an order does not increase stock.
- **Purchase List:** receipt-based list only. When good/leakage items are received against a pending/partial order, a separate `PUR-00001` style purchase invoice is generated. Good quantity alone increases physical stock. Both order and purchase receipt have **View Invoice**.
- **Remove SKU entry:** new product form and stock table no longer show SKU (historic demo data may still contain an unused SKU field).
- **Unused Points:** filter by date, invoice number or customer name; marking a given invoice used keeps that invoice fixed in the dialog.
- **Customer Dues:** opening a dues receipt from an invoice keeps the invoice fixed, displays its details, and prevents accidental switching.
- **Product Delivery:** removes the `Billed` column/label from the Product Delivery and Pending Delivery views while retaining quantities internally.
- **Returns/Refund/Exchange:** search and open invoice, see all products, enter per-product return quantities or use All Return, see return value/refund, and choose Cash or Bank for refund deductions. Damaged returns do not restock. Exchange is a *return record demonstration*; replacement dispatch is not automatically finalized.
- **Leakage Replacement:** opening a company invoice displays all outstanding leakage products for that invoice; enter good replacement quantities per product. Only accepted good replacements restock.

### Testing and limitations

JSX parsing and transpilation passed via the TypeScript parser available in the build environment. The app was also rendered with a lightweight virtual-React test harness against **15 pages and 8 dialogs**, with no render exceptions found. A real `npm run build` could **not** be completed in this environment because `npm install` timed out; Vercel deployment is not guaranteed until a full Vite build runs on your deployment environment. The temporary test harness is **not** part of the delivered project.

Vercel is configured to **clean-install Linux dependencies**, build using `node ./node_modules/vite/bin/vite.js build`, and publish the Vite `dist` directory. The ZIP intentionally contains no `node_modules` or `dist` folder.

> Demo-only: Data is kept in this browser's localStorage. It is not financially/audit safe, multi-user synchronized, real WhatsApp connected, or ready for production use.
