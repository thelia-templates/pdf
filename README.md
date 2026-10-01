# Thelia default PDF template

The default PDF template of Thelia 3, rendered with Twig and converted to PDF
by dompdf.

It contains four documents:

- `invoice.html.twig` — customer invoice
- `delivery.html.twig` — delivery note
- `order_return.html.twig` — return document of an order return
- `credit-note.html.twig` — credit note of the [CreditNote module](https://github.com/thelia-modules/CreditNote)

All of them are self-contained HTML with an embedded stylesheet: dompdf supports
only a subset of CSS, so keep the styling simple.
Translations live in `translations/`, under the `pdf` domain.

## Compatibility

- Thelia 3.1 or later (`thelia/core` ^3.1), TwigEngine 1.0.9 or later
- PHP 8.3+
- The credit note document needs the CreditNote module, Thelia 3 line

## Layout

The documents are laid out to keep the printed page count down:

- the full store imprint (address, country, business id, phone, email) is printed
  once, next to the document information on the first page. It is what the
  `invoice.imprint` hook (`credit-note.imprint` on the credit note) replaces when
  a module provides one;
- the running footer repeated on every page is condensed to a single line
  (store name, city, business id) plus the page number;
- each order line uses a two-line cell: the product title, then a smaller line
  carrying the references and the combination. The sale element reference is
  printed only when it differs from the product reference.

## Language

A document is printed in the language the order was placed in, not in the
language of whoever prints it: the customer is the one who keeps it. The invoice
and the delivery note read it on the order; the credit note takes the language the
module asks for, otherwise the one of the order it refunds. A credit note without
order and without a requested language is printed in the language of the page.

## The credit note document

The CreditNote module renders `credit-note` from the active PDF template with
`credit_note_id`, and may add `document_locale` (the language to print in, the one
its customer prefers) and `credit_note_type_title` (the type of the credit note in
that language, since the loops translate in the language of the session). Without
`document_locale`, the document is printed in the language of the refunded order.
Everything else is read through the loops of the module (`credit-note`,
`credit-note-detail`, `credit-note-address`) and of the core (`order`,
`order_product`, `customer`, `country`, `title`).

The document prints:

- the credit note reference (`ref`) and, when the module assigned it, the
  accounting number of the credit note (`invoice_ref`): two distinct numbers,
  neither of them the invoice number of the order;
- the date, the customer number, the credit note type, and for a credit note
  attached to an order its reference and the original invoice number;
- the store imprint and its legal identifiers, as on the invoice;
- the invoice address frozen on the credit note when it was issued. A module
  that does not expose `INVOICE_ADDRESS_ID` on its `credit-note` loop gets the
  invoice address of the order instead;
- one row per line: title, product references and combination when the line
  comes from an order product, unit price without tax, tax rate, unit price with
  tax, quantity, total with tax. The rate is derived from the two unit prices of
  the line, so a free line or a shipping line prints its own rate;
- the summary: the total without tax of the lines, one tax row per rate met on
  the lines (with the taxed base), the discount without and with tax when the
  credit note carries one, then the total tax amount and the total with tax the
  module stored on the credit note.

Only an accepted credit note is served by the module, so the status is not
printed.

### Hooks

Every hook receives `credit_note`, the id of the credit note.

| Hook | Where |
|---|---|
| `credit-note.css` | Inside the stylesheet |
| `credit-note.header` | Above the document |
| `credit-note.footer-top` | Above the running footer |
| `credit-note.imprint` | Replaces the store block when it answers |
| `credit-note.information` | Block hook: `title` / `value` fragments added to the information rows |
| `credit-note.after-information` | Below the information block |
| `credit-note.after-addresses` | Below the invoice address |
| `credit-note.detail` | Inside the first cell of each line (`credit_note_detail`, `order_product`) |
| `credit-note.after-detail` | After each line (`credit_note_detail`) |
| `credit-note.after-products` | Below the lines table |
| `credit-note.notice` | Left of the summary, for a usage notice |
| `credit-note.after-summary` | Below the summary |

## Customization

Do not edit this template in place: an update will overwrite your changes.
Copy it to `templates/pdf/<your-template>` and select it in the back office,
or override only the files you need to change.

## Documentation

https://doc.thelia.net

## License

GPL-3.0-or-later
