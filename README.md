# Madras Mami – Daily Closing Report

A single-page web app for closing the till at **Madras Mami Brampton**. It replaces the paper/spreadsheet closing sheet and is designed to be mistake-proof.

Everything is in one file: `index.html`. No build step, no server.

## What it does

### Closing report (staff)
1. **Sales** – enter Net sales, Cash sales and Cash tips.
2. **Till count** – enter how many of each bill and coin are in the till. Totals update live.
3. **Expenses** – add each expense by vendor, with an amount and a **receipt photo** (required).
4. **Result** – shows what the till should have, what was counted, and the difference (over / short).
5. **Envelope** – the amount to put in the envelope is filled in automatically. It can be lowered (or rounded down to $5 / $10 / $20 / $50) to keep extra change in the till.
6. **Wastage, notes, Toast report photo** – optional notes, plus a photo of the Toast sales printout (required).

The **Create closing report** button stays locked until every check passes (closer's name, sales, till counted, all receipts attached, Toast photo, reason for any difference).

When the report is created you can:
- **Share all to WhatsApp** – the closing report image, expense receipts and Toast report, in that order.
- **Save all images** – download them instead.

### How the till math works
- **Opening till** = the till amount left by the previous report (first report: $500, or whatever is entered).
- **Till should have** = opening till + cash sales − expenses.
- **Difference** = counted − should have.
- **Default envelope** = counted − standard till ($500). If the till opened below $500, today's cash tops it up first and only the surplus goes in the envelope.
- **Left in till** = counted − envelope. This becomes tomorrow's opening till (so $500 plus any extra change you chose to keep).
- Cash tips are shown on the report but are **not** part of the till math.
- Count the till **after** expense cash has been taken out.

### Manager tab (PIN protected)
- Weekly (Mon–Sun), bi-weekly and monthly views, with previous / next period.
- Net sales, cash sales, tips, expenses, cash added to the envelope, till over / short.
- **Cash on hand** at period end (envelope balance + till).
- Expenses by vendor and a day-by-day table.
- Warning for days with no report.
- Record cash taken out of the envelope (bank deposit, payroll, etc.).
- Share the summary as an image or download it as CSV.
- Settings: standard till amount, bi-weekly start date, change PIN, backup and restore.

## Where the data is stored (important)

There is no server or database. Reports are saved in the **browser of the device used to close** (`localStorage`).

- Always close from the **same phone or tablet** so the till balance carries over correctly.
- Use **Manager → Backup all data** regularly. Use **Restore from backup** to move to a new device.
- Clearing browser data erases the history.
- Receipt and Toast photos are **not** stored in the app; they are only used to create the images you share.
- The manager PIN is a convenience lock, not real security.

## Deploy on GitHub Pages

1. Create a repository and upload `index.html` (and this `README.md`) to the root.
2. Go to **Settings → Pages**, choose your main branch and the `/ (root)` folder, then save.
3. The app is live at `https://<your-username>.github.io/<repository-name>/`.
4. On the phone, open the link and choose **Add to Home Screen**.

HTTPS (which GitHub Pages provides) is needed for camera access and the WhatsApp share sheet.

## Notes

- Loads two things from the internet: the `html2canvas` library (cdnjs, used to make the report image) and the Montserrat font (Google Fonts). A connection is needed when the app is used.
- Branding follows the Madras Mami brand guidelines: emerald green `#14573a`, gold `#dbb640`, mud brown `#452e18`, off-white `#f2ebd6`.
- The logo is embedded in `index.html` as an image, so there are no other files to upload.
- Browser sharing of several images at once works on most phones; if it isn't supported, the app downloads the images instead.
