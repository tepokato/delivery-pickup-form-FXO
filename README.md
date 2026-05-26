# Delivery pickup form (FedEx Office)

Internal web form for FedEx Office staff to record package pickup or delivery requests and produce a PDF summary for coordination with warehouse partners and store operations.

The application is a single HTML document (`index.html`) that runs entirely in the browser. Layout, styling, form logic, embedded icons, and PDF generation live in that one file. PDF output uses [jsPDF](https://github.com/parallax/jsPDF) loaded from a public CDN.

## Purpose

Staff use the form at the counter to capture who is requesting service, what is being moved, where packages are located, and how payment is handled. After the required fields are complete, the form downloads a PDF that can be shared or filed. Employee name and badge number are collected so partners can follow up if guest or package details were missed on the form.

## How it works

### Request flow

1. **Staff information** — Employee name and badge number (required).
2. **Guest information** — Optional guest name, phone, and company.
3. **Request type** — Pickup or delivery. Choosing one type shows only the fields that apply; the other panel stays hidden.
4. **Payment** — Paid or will pay later, optional FedEx account number, and a checkbox if credit card details were collected (with a note that card data is stored in the safe, not on this form).
5. **Download PDF** — Submits the form in the browser, runs validation, then generates and saves a PDF. **Clear form** resets all inputs after confirmation.

Validation runs before PDF creation. Errors appear in a banner at the top of the card and on individual fields. The first invalid field receives focus when possible.

### Pickup

When pickup is selected, staff can enter:

- Number of packages (drives how many weight fields appear)
- Package location (dropdown from the shared location list)
- Booth number or letter
- Weight per package (one text field per package, generated from the package count)
- Pickup date and pickup time (free text)

Pickup requires a package location and a weight for each package when the package count is at least one.

### Delivery

When delivery is selected, staff can enter:

- Number of packages (drives how many weight fields appear)
- Package storage location (dropdown)
- Weight per package (one text field per package)
- Delivery date and delivery time (free text)
- Final delivery location (dropdown)

Delivery requires storage location, final delivery location, and a weight for each package when the package count is at least one.

### Package weights

Entering a package count builds a matching number of weight inputs. Changing the count rebuilds the list while preserving values for indices that still exist. Weights are listed in the PDF as one line per package (for example, `Package 1: 5 lbs`).

### Locations

Pickup package location, delivery storage location, and final delivery location share one maintained list. Default entries are seeded on first use; staff can add new location names inline. Added names are title-cased, stored in the browser’s `localStorage`, and merged into all relevant dropdowns. Duplicate names are rejected.

### PDF output

The generated file is plain text formatted by jsPDF: a single title (“FedEx Office - Package Request Form”), a general information block (staff, guest, request type, payment), then either pickup or delivery details depending on the selection. The file is always named `FedEx_Package_Request_Form.pdf`.

Pickup and delivery sections include package count, locations, booth (pickup only), weights, dates, and times as entered on the form.

### Interface

The UI uses a FedEx-oriented purple and orange theme, a centered card layout, and numbered sections. Pickup and delivery are chosen with large radio controls that show embedded pickup and delivery icons. Section headings for pickup and delivery details repeat those icons.

A fixed action bar on narrow viewports keeps **Download PDF** and **Clear** visible while scrolling. Wider screens show the same actions inside the card footer.

Icons (FedEx Office mark, pickup, delivery) are embedded in the HTML as SVG symbols referenced with `<use>`, so no separate image files are required beside `index.html`.

## Technical notes

- No backend: data never leaves the browser except when the user saves the PDF.
- Location persistence is per browser and per origin (`localStorage` key `fxo_package_form_locations`).
- Maximum package count for weight fields is capped at 50.
