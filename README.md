# 📦 Delivery pickup form FXO

This web-based application streamlines the process of submitting package pickup or delivery requests at FedEx Office locations. Designed for internal staff use, the form allows employees to input essential information about the guest, package details, and request type, then generate a neatly formatted PDF for recordkeeping or operational coordination.

🔧 Features
- Pickup or Delivery: Segmented control reveals the matching detail fields.
- PDF export: Auto-generates a printable summary using jsPDF.
- Inline validation: Errors appear at the top and on fields before PDF download.
- Location management: Preloaded locations plus inline add; custom entries persist in the browser (localStorage).
- Mobile-friendly layout: Sticky action bar and two-column fields on wider screens.
- FedEx-themed UI: Purple and orange palette for familiarity and clarity.

📝 Required Fields
- Employee name
- Badge number
- Request type (Pickup or Delivery)
- Location dropdowns for the selected request type

🚀 Getting Started
To use the form:

1. Open `index.html` in any modern web browser (or serve the folder with a simple static server).
2. Fill in staff and guest details.
3. Select Pickup or Delivery and complete the detail section.
4. Click **Download PDF** to generate the form summary.

🔐 Note on Payment Info
If credit card information is collected, the checkbox will be marked, and a note will indicate that this information is securely stored offline.
