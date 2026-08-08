# Thelia default PDF template

The default PDF template of Thelia 3, rendered with Twig and converted to PDF
by dompdf.

It contains two documents:

- `invoice.html.twig` — customer invoice
- `delivery.html.twig` — delivery note

Both are self-contained HTML with an embedded stylesheet: dompdf supports only
a subset of CSS, so keep the styling simple.
Translations live in `translations/`, under the `pdf` domain.

## Customization

Do not edit this template in place: an update will overwrite your changes.
Copy it to `templates/pdf/<your-template>` and select it in the back office,
or override only the files you need to change.

## Documentation

https://doc.thelia.net

## License

GPL-3.0-or-later
