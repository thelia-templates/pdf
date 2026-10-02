# Changelog

All notable changes to this template are documented here.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and the template adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- The invoice prints, under the reference of each line, the GTIN and the manufacturer part number of the item as they were when the order was placed. Nothing is printed for a line that has neither. The part number needs a core that freezes it on the order line; with an older core the GTIN alone is printed.
- English and French labels of the two codes.

## [1.2.0] 2026-09-22

The credit note becomes the fourth document of the template.

### Added
- `credit-note.html.twig`, the printable credit note of the CreditNote module: the credit note reference and its accounting number, the order and the original invoice it refunds, the customer number, the credit note type, the store imprint and legal identifiers, the invoice address frozen on the credit note, one row per refunded line with its unit prices and tax rate, the taxes gathered by rate, the discount when there is one, and the totals the module stored. The document is printed in the language the module asks for (`document_locale`, the language its customer prefers), otherwise in the language of the refunded order; the module may also hand over the title of the credit note type in that language (`credit_note_type_title`).
- Hooks of the credit note document, every one of them handed the credit note id: `credit-note.css`, `credit-note.header`, `credit-note.footer-top`, `credit-note.imprint`, `credit-note.information` (block, `title` and `value` fragments), `credit-note.after-information`, `credit-note.after-addresses`, `credit-note.detail`, `credit-note.after-detail`, `credit-note.after-products`, `credit-note.notice`, `credit-note.after-summary`.
- English, French, German, Spanish, Italian and Dutch labels of the credit note document.

### Fixed
- The English catalog lacked the "Postage without tax" label the invoice prints.

## [1.1.0] 2026-09-16

### Added
- `order_return.html.twig`, the return document a customer slips into the parcel.

### Changed
- Requires Thelia core 3.1 and TwigEngine 1.0.9.
- The invoice and the delivery note are printed in the language of the order, not in the language of whoever prints them.

## [1.0.0] 2026-08-24

First release of the Twig template, rendered by dompdf.

### Added
- `invoice.html.twig` and `delivery.html.twig`, ported from the Smarty template of Thelia 2.
- The store legal identifiers (SIRET, APE code, VAT number, EORI, exemptions, free-text mentions) on both documents, and the legal identifiers of the invoice address on the invoice.
- The customer discount rate on the invoice.
- Translation catalogs of the `pdf` domain for the Twig `trans` filter.

### Changed
- The store imprint is printed once, next to the document information, and the running footer is condensed to a single line, to keep the printed page count down.

[1.2.0]: https://github.com/thelia-templates/pdf/releases/tag/1.2.0
[1.1.0]: https://github.com/thelia-templates/pdf/releases/tag/1.1.0
[1.0.0]: https://github.com/thelia-templates/pdf/releases/tag/1.0.0
