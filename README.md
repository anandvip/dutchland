# Dutchland Order Book

A single-file, offline-first ordering page for a repeating monthly order. You enter items, quantities, prices and shipping; the page totals the order, opens WhatsApp with the order typed out for your supplier, and keeps a year-by-year account in the browser.

- **Created:** 10 November 2026
- **Tool:** Claude (Fable 5.2, Anthropic)
- **Stack:** plain HTML, CSS and JavaScript in one `index.html`. No frameworks, no CDN, no build step.

## What it does

| Tab | Purpose |
| --- | --- |
| **Order** | Itemized order form (item, qty, unit, price per unit), shipping charges, note. Live totals. "Save and send on WhatsApp" stores the order and opens a chat with the supplier with the message filled in. |
| **Year account** | Calendar-year (Jan to Dec) totals, a month-by-month bar chart, every saved order with its lines, "Order this again", delete, and CSV export. |
| **Setup** | Supplier name and WhatsApp number (saved once), your name and delivery address. |

## Behaviour worth knowing

- **Remembers the last order.** After an order is saved, the next one opens prefilled with the same items and prices.
- **No double counting.** An order is saved once, at the moment you press save. The page then shows a "saved" card; re-opening WhatsApp from there does not save again.
- **Money is held in paise** (integers), so totals do not drift from floating-point rounding. Display uses ₹ and the en-IN format.
- **WhatsApp number:** a 10 digit number is treated as Indian (+91). Include the country code for other countries. The page only opens WhatsApp with the text ready; you press send there.
- **CSV export:** one row per item and one separate row for shipping, so the `Amount (INR)` column sums to the year total. The file carries a UTF-8 BOM and opens in Numbers and Excel. "Copy CSV" is the fallback where downloads are blocked.
- **Storage:** everything lives in `localStorage` under the key `dutchland.v1`, per browser and per device. Clearing site data removes it, so export the CSV as a backup.

## Run it

Open `index.html` in a browser, or host it on GitHub Pages.

## Prompt used

> Let's create an itemized ordering application. which finally spits the items entered by the user so assuming user knows the price of items and quantity and shipment charges. Simple plain vanilla js application uses local storage and remembers the last order. Takes the WhatsApp number and sends the order to that whatsapp number orders are repetitive each month so yearly account must be maintained in the local storage and even exportable as CSV to the numbers app or Excel as a back up. save the application to artifact too. And if possible create a repo at GitHub by the name dutchland and publish the GitHub page after saving it as index.html and share the link after publishing. any questions? Keep the styles minimal and remember functionality proceeds, form decorate it with modern good looking design and svg images.

Clarifications given: one fixed supplier, calendar-year account, new order prefilled from the last one, generic artwork.
