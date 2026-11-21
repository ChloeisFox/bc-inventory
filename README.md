# Between Chapters Inventory: setup

Three parts work together. The phone app lives on GitHub Pages, your inventory lives in a Google Sheet, and a small Apps Script attached to the sheet saves books and checks eBay prices. Your passwords and eBay keys stay inside Apps Script, so the GitHub repo can be public safely.

## 1. Make the Google Sheet

1. Create a new Google Sheet named "Between Chapters Inventory".
2. Go to **Extensions > Apps Script**. Delete the starter code, paste in everything from `Code.gs`, and click Save.
3. In the function dropdown at the top, pick `setup` and click **Run**. Approve the permissions Google asks for. Your sheet now has an Inventory tab with headers.
4. Click the gear icon (**Project Settings**), scroll to **Script Properties**, and add:
   - `APP_KEY` with any password you make up. You'll type this into the app once.

## 2. Publish the script as a web app

1. Click **Deploy > New deployment**. Choose type **Web app**.
2. Set **Execute as: Me** and **Who has access: Anyone**.
3. Click Deploy and copy the **Web app URL** (it ends in `/exec`).

If you ever change the script code, use **Deploy > Manage deployments**, click the pencil, choose **New version**, and Deploy. The URL stays the same.

## 3. Get free eBay keys (for automatic prices)

1. Sign up at developer.ebay.com with your eBay account.
2. Go to **Application Keys** and create a **Production** keyset. eBay will ask about "Marketplace account deletion notifications." Since this app never stores eBay user data, choose the option to request an exemption.
3. Copy the **App ID (Client ID)** and **Cert ID (Client Secret)**.
4. Back in Apps Script Script Properties, add `EBAY_APP_ID` and `EBAY_CERT_ID` with those values.
5. Pick `testEbay` in the function dropdown and click Run. Open **Execution log** and you should see prices for a test book.

The app works without eBay keys. You'll still get title, author, and cover lookups plus the quick price buttons.

## 4. Put the app on GitHub Pages

1. On GitHub, create a new repository, for example `bc-inventory`.
2. Click **Add file > Upload files** and upload `index.html` and `sw.js` (and this README if you like). Commit. `sw.js` is what lets the app open with no signal.
3. Go to **Settings > Pages**. Under Source, choose **Deploy from a branch**, branch `main`, folder `/ (root)`. Save.
4. After a minute your app is live at `https://YOUR-USERNAME.github.io/bc-inventory/`.

## 5. Set it up on your phone

1. Open the link in Safari, tap Share, then **Add to Home Screen**.
2. Open the app, tap the **gear icon** for Settings, paste the web app URL and your APP_KEY, and tap **Save and test connection**.
3. On the **Add** tab, tap **Start camera** and allow camera access.
4. While you're in Settings, pick your color (green or purple), light or dark mode, and your county for sales tax.

## Colors and dark mode

In Settings (gear icon), under **Look**, pick Green or Purple and choose Light, Dark, or Match my phone.

## Selling at a booth

The app opens on the **Sell** tab.

1. Type the event name at the top (like "PSL Farmers Market") and pick the type, such as Booth. The app remembers both until you change them.
2. Tap **Scan books to sell** and scan each book. The camera stays on so you can scan a stack. You can also type a BC number (just "12" works for BC-0012), an ISBN, or part of a title.
3. If you have more than one copy of a book, the app asks which one.
4. Change a price in the cart to give a discount.
5. Pick Square, Cash, Zelle, or Other. For cash, type what they handed you and the app shows the change.
6. Tap **Complete sale**. Every book is marked sold with the price, tax, payment, event, and date.

**Undo last sale** puts those books back in stock if you made a mistake.

Square note: the app records that a sale was paid with Square, but it doesn't connect to Square. Ring up the total on your Square reader as usual.

## Sales tax

In Settings (gear icon), pick the county you're selling in that day. Florida charges 6% state tax plus the county surtax where the customer gets the book, so a market in Martin County uses Martin's rate even though you live in St. Lucie. The 2026 surtax rates are filled in: St. Lucie 1%, Martin 0.5%, Indian River 1%, Palm Beach 0.5%. Pick Other to type a different county's rate.

Check **My prices already include tax** if you'd rather price books at round numbers like $5 with tax built in. The app then works backward to figure the tax portion.

The Sales tab has a **Sales tax report** for this month, last month, this quarter, or this year. It shows what you collected, taxable sales, and tax collected, split by county, payment type, and event, and downloads as a CSV. Florida's Department of Revenue publishes the next year's county rates each November, so check them before January 1.

## Boxes, shelves, and tables

Every book has a **storage box** (like "Box 2") where it lives when it isn't out. **Right now** says whether it's in its box or out on a shelf or table, and which one (like "Table 1").

On the Shelf tab, open **Set up or pack up for a market**:
- **Set out every book from this box** marks a whole box as out on the table or shelf you type.
- **Pack up** puts every book that's out back into its own box.

The location filter on the Shelf tab can show everything that's out, everything on one table, or everything that belongs in one box. The checkout cart shows where each copy is.

## Planning your boxes

On the Shelf tab, open **Plan my boxes**. Enter how many boxes you have and about how many books fit in one, then tap **Suggest a plan**.

- Kids' books (Children's, Middle Grade, and Young Adult) are grouped by age rating, youngest first.
- Everything else is grouped by genre, in the same order as the genre list, so related genres like Romance and Romantasy end up near each other.
- A genre stays together in one box when it fits. A genre too big for one box spills into the next box.
- Within each box, books are in order by author.
- The plan shows what goes in each box and which books need to move. If your boxes can't hold everything, it tells you how many more you'd need.

Tap **Use this plan** to update every book's storage box. Run it again any time your stock changes.

## Where you got each book

**Where I got it** has choices like My library, Website, Bookstore, and Used sale, plus a box for the website or seller (ThriftBooks, Amazon, and so on). Along with **I paid**, this feeds the profit numbers on the Sales tab.

## Working offline

Every change saves on your phone first and goes to the Google Sheet as soon as there's signal. The top corner shows how many changes are waiting. New books get a temporary ID like NEW-K3FA until they reach the sheet, then switch to a BC number. Download bookmark files after everything has synced so the IDs are final.

Open the app once while online after each update so your phone saves the newest version.

## Making bookmarks in Canva

Bulk Create works on a computer (Canva desktop app or canva.com in a browser), so do this part there. You can open the inventory app on your computer too; it's the same GitHub link.

**Set up your templates once**

1. Build the Library Card design in Canva (2 x 6 in) with a text box for each of these columns: Price, Title, Author, Age Rating, Stars, Rating Number, Spice Peppers, Blurb, and Book ID. Use placeholder text sized for a long title and a 240-character blurb. Put your logo, the Between Chapters name, the "Read by" lines, and your QR code on the back.
2. Make a copy of the design for each genre you stock and change its color to match the genre's color in the app (the hex codes are in `GENRES` in index.html, for example Romance `#F7C6D0`).
3. Name each copy by genre, like "Bookmark: Romance."

**Each time you print**

1. In the app, open the **Bookmarks** tab. It lists in-stock books that are new or changed since their last bookmark, grouped by genre.
2. Tap **CSV** next to a genre, or **Download all genres (zip)** and unzip it.
3. In Canva, open that genre's template, go to **Bulk create > Upload data**, and pick that genre's CSV.
4. Connect each text box to its column, preview a few, and generate.
5. After printing, tap **Printed** next to the genre (or **Mark all as printed**) so those books drop off the list.

**How the bookmark list stays current**

- New books start as needing a bookmark.
- Changing a book's price, title, author, genre, age rating, spice, condition, rating, format, or blurb puts it back on the list.
- In a book's editor you can also check or uncheck **Needs a new bookmark** yourself.
- Sold books never show on the list.
- Canva takes up to 300 rows per upload, so a genre with more books than that downloads in parts.
- The Stars column uses star symbols (★★★★☆), rounded to the nearest whole star, and Rating Number has the exact rating.
- The Spice Peppers column uses pepper emoji, which some Canva fonts don't show. Test one bookmark first. If they come out blank, use the Spice column ("Spice 3/5") next to one pepper graphic.
- Leave Spice Peppers empty on templates for genres where you don't track spice.

**Blurbs**

The blurb comes from the publisher's description through Google Books or Open Library, the same back-cover copy Amazon and Barnes & Noble use. The app takes the first few sentences that fit in 240 characters, skipping lines like "#1 bestseller" and review quotes. To change it, open **Pick sentences from the publisher description** and tap the sentences you want, or type your own. If a book has no description, copy a line from the back cover.

**Book IDs**

Every book gets a short ID like BC-0001 to print on the bookmark.

## Using a Bluetooth scanner

Pair the scanner in your phone's Bluetooth settings (keyboard or HID mode). Tap the ISBN box on the Add tab (or the search box on the Sell tab), then scan. The scanner types the number and presses Enter for you.

## Good to know

- The eBay numbers are prices on used copies listed for sale right now. For what copies actually sold for, tap the **eBay sold** button.
- Prices for the same ISBN are reused for an hour so repeat scans are instant.
- Mass-market paperbacks often have a store UPC on the back. The ISBN barcode is usually inside the front cover.
- Books from before about 1970 may have no ISBN. Use **Add a book without an ISBN**.
- Every field you enter saves to the sheet automatically, including pages, genre, description, and both ratings. Settings has an **Open my Google Sheet** button once you connect.
- Goodreads shut down its public API in 2020, so the app can't fill in Goodreads ratings by itself. Tap **Find on Goodreads**, then type the rating in. Open Library's reader rating fills in automatically.
- Genres are color-coded in the app and in the sheet. Running `setup` again recolors any rows you typed into the sheet by hand. To change a color, edit it in both `GENRES` (index.html) and `GENRE_COLORS` (Code.gs).
- Genre and age rating are suggested from the categories Google Books and Open Library list for the book. Spice has no free data source, so you pick it, with a Romance.io button to check reader ratings. Common Sense Media is linked for kids' and teen books.
- You can edit the Google Sheet directly. Tap **Refresh inventory from sheet** in Settings to pull your edits into the app.

## Updating later

After you're set up, when I send you new versions: paste the new `Code.gs` over the old one, Save, run `setup` once (it adds the new column headers without touching your books), then **Deploy > Manage deployments > pencil > New version > Deploy**. Upload the new `index.html` (and `sw.js` if it's not there yet) to GitHub to replace the old ones.
