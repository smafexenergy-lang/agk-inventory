AGK INVENTORY: POS & INVENTORY (Installable Web App)
==============================================================

WHAT THIS IS
This is a Progressive Web App (PWA). Once hosted, it can be "installed"
on a PC or phone like a real app: its own icon, its own window, works
offline, no browser address bar.

IMPORTANT: THIS WON'T INSTALL IF YOU JUST DOUBLE-CLICK index.html
Browsers block the "Install" feature and offline caching on files opened
directly from disk (file://). The app needs to be served over http:// or
https://, even a local server counts. Three easy ways to do that:

OPTION 1: Free permanent hosting (recommended)
  1. Create a free account at https://pages.github.com or https://app.netlify.com
  2. Drag this whole folder onto the Netlify "Deploy" drop zone
     (or push it to a GitHub repo and enable GitHub Pages).
  3. Open the resulting https:// link on your PC or phone.
  4. PC (Chrome/Edge): click the install icon in the address bar, or the
     "Install App" button inside the tool.
     Phone: browser menu → "Add to Home Screen" / "Install App".

OPTION 2: Run it locally on your own PC (no internet needed after setup)
  1. Install Python (most PCs already have it) or Node.js.
  2. Open a terminal/command prompt in this folder.
  3. Run:  python -m http.server 8080
           (or, with Node:  npx serve .)
  4. Open http://localhost:8080 in Chrome or Edge.
  5. Click "Install App" (or the install icon in the address bar).
  6. From then on, launch it like any installed app. The local server
     only needs to be running the first time you install it; after
     installation the app works offline.

OPTION 3: Company/local network hosting
  If you have a shared PC, small server, or hosting account already,
  just upload this folder there and open the URL from any device on
  that network, same install steps as Option 1.

RECEIPT SIZE (reverted)
Based on feedback, receipts and quotations are back to the wider,
better-looking layout (roughly a compact A5-style card, ~420px)
instead of the narrow 80mm thermal-receipt width tried earlier. They
still print on a single page with no extra blank pages.

TOP NAVIGATION (replaces the old collapsible sections)
The app is now organized into proper pages with a navigation bar
under the header:
  🏠 Dashboard — search, cart, quick stock update, KPIs, top sellers,
     charts. This is what opens by default.
  🏷️ Categories — buttons for each product category; click one to
     see just that category's products and add them straight to the
     cart from there.
  📋 Quotations — build and manage price quotes.
  🧾 Transactions — search and filter your sales history, print or
     void past sales.
  📦 Products — the full product database: add, edit, delete, export.

Each nav button (except Dashboard) shows a small live count badge, so
you can see at a glance how many products, transactions, or
quotations exist without opening the page. Only one page shows at a
time, which is what keeps the screen short and focused now instead of
one long scroll.

LOADING SPLASH SCREEN
When you open the app, a branded loading screen (logo, "AGK
Inventory", a four-square pulsing loader) shows for about 15 seconds
before revealing the dashboard. Your data is actually loaded well
before that in the background, so the delay is purely presentational
branding, not a technical wait. If 15 seconds feels too long
day-to-day, this is a single number in the code (SPLASH_DURATION_MS
near the very end of index.html) that's easy to shorten, just say the
word and I'll adjust it.

RECEIPT & QUOTATION BRANDING
Each printout shows Heritage Traders (HT) with the logo, contact
details, and: a receipt number, date and time, itemized lines, total,
item count, payment method, amount received and change due (for cash
sales), and a QR code. The app also temporarily renames the browser
tab/print title to match the receipt or quotation number while
printing, so nothing referencing "AGK Inventory" appears in your
browser's print header or in a saved PDF's filename.

If your browser still shows its own header/footer (date, URL, page
number) at the very edges when printing, that's a browser setting,
not something in the app: open the print dialog's "More settings" and
uncheck "Headers and footers" to remove it.

PAYMENT METHOD & CHANGE DUE
At checkout, choose a payment method (Cash, Mobile Money, Bank
Transfer, or Card). For Cash, enter the amount received and the
change due calculates and displays live, then prints on the receipt
automatically.

DASHBOARD LAYOUT
The Dashboard page has two columns: search, cart, and checkout on the
left; Quick Stock Update and Top 5 Best Sellers on the right. Use
"Quick stock update" for fast day-to-day adjustments (type a code,
set a new number or use +10/-10, save) without needing to open the
full Products page. The two donut charts (revenue by category, stock
status) that used to sit here have been removed to keep the page
shorter and cleaner.

PRINTING
Receipts and quotations now print cleanly on a single page, with
Heritage Traders (HT) branding and contact details at the top
(heritagetraders@gmail.com, 0999925883, Lilongwe, Malawi). Note this
business name is used specifically on printed documents; the app
itself is still called AGK Inventory.

RECEIPTS & QUOTATIONS
Every completed sale automatically opens a printable receipt (with a
QR code encoding the transaction ID, date, and total). You can also
reprint any past sale's receipt from the "Receipt" button on the
Transactions page.

The Quotations section lets you build a price quote for a customer
(search products, set quantities, optional customer name and valid
until date) without touching stock. Generate it to get a numbered,
printable quotation (also with a QR code), saved to a history list
where you can view/print it again, delete it, or click "To sale" to
push its items into the cart and complete it as a real sale.

QR codes are generated entirely offline (no internet needed) using a
small vendored library, so this works even without a connection.

MANAGER PASSCODE (team protection)
Click "⚙ Manager Settings" in the top bar to set a passcode. Once set,
deleting a product or voiding a sale will ask for that passcode before
completing. This stops team members from undoing sales or removing
products without approval, while everyone can still search, sell, and
add new products freely.
  - The passcode is a simple shared deterrent, not encryption. Anyone
    with the passcode (or direct access to the stored data) can bypass
    it, so treat it like a shop-floor PIN, not a bank password.
  - It syncs via Google Drive along with your product/sales data, so
    it's the same passcode across every device you connect.
  - To change or remove it later, click Manager Settings again and
    enter the current passcode first.

DATA & BACKUPS
Product and sales data is stored locally in the browser/app on each
device. It does NOT sync between devices, UNLESS you connect Google
Drive (see below). Use the "Export products (CSV)" and "Export sales
log (CSV)" buttons any time for a plain backup, and to move data
between devices if needed.

GOOGLE DRIVE SYNC
Click "Connect Google Drive" in the top bar and sign in with the same
Google account you used to set up the project in Google Cloud Console
(it must be added as a test user there). Once connected:
  - Your data is saved to a file called heritage-investments-data.json
    in your Drive automatically, a couple of seconds after any change.
  - Opening the app on another device and connecting the same Google
    account pulls that data back down.
  - You stay signed in only for that browser session. Connect again
    next time you open the app (this is expected with a Testing-mode
    Google Cloud project).
Note: this data lives in your own Drive, not visible to anyone else
unless you share the file yourself.

FILES IN THIS FOLDER
  index.html         The app itself
  manifest.json       Tells the browser how to install it (name, icon, colors)
  service-worker.js   Makes it work offline once installed
  icon-192.png / icon-512.png   App icons
