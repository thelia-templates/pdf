# Thelia default PDF template

The default PDF template of Thelia 3, rendered with Twig and converted to PDF
by dompdf.

It contains two documents:

- `invoice.html.twig` — customer invoice
- `delivery.html.twig` — delivery note

Both are self-contained HTML with an embedded stylesheet: dompdf supports only
a subset of CSS, so keep the styling simple.
Translations live in `translations/`, under the `pdf` domain.

## Layout

Both documents are laid out to keep the printed page count down:

- the full store imprint (address, country, business id, phone, email) is printed
  once, next to the document information on the first page. It is what the
  `invoice.imprint` hook replaces when a module provides one;
- the running footer repeated on every page is condensed to a single line
  (store name, city, business id) plus the page number;
- each order line uses a two-line cell: the product title, then a smaller line
  carrying the references and the combination. The sale element reference is
  printed only when it differs from the product reference.

## Customization

Do not edit this template in place: an update will overwrite your changes.
Copy it to `templates/pdf/<your-template>` and select it in the back office,
or override only the files you need to change.

## Documentation

https://doc.thelia.net

## License

GPL-3.0-or-later
