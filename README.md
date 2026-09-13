# Tahanoa Invoice Links for ZarinPal

<img width="1672" height="941" alt="Tahanoa Invoice Links for ZarinPal" src="https://github.com/user-attachments/assets/82f7c275-00da-46e2-884a-a1f92f051615" />

![WordPress](https://img.shields.io/badge/WordPress-Plugin-blue)
![Version](https://img.shields.io/badge/version-1.5.9-green)
![PHP](https://img.shields.io/badge/PHP-7.4%2B-777BB4)
![License](https://img.shields.io/badge/license-GPL--2.0--or--later-orange)

A secure WordPress plugin for creating payment-link invoices with custom amounts or WooCommerce products and accepting payments through ZarinPal.

> Tahanoa Invoice Links for ZarinPal is an independent integration. It is not affiliated with, endorsed by, or sponsored by ZarinPal.

## Features

- Create invoices with a manually entered amount.
- Search WooCommerce products by name or SKU and add quantities.
- Generate unique public payment links.
- Add customer name, mobile number, email, and invoice description.
- Configure an optional fixed shipping fee per invoice.
- Use ZarinPal API v4 Request, Verify, and Inquiry endpoints.
- Confirm payments only through server-to-server verification.
- Retry verification from the WordPress dashboard after temporary failures.
- Store optional redacted debug logs with sensitive data excluded.
- Export and erase customer contact data through WordPress Privacy Tools.
- Keep invoice pages inside the active WordPress theme.

WooCommerce is optional. The plugin can create manual-amount invoices without it.

## Security

- Capability checks for administrative actions.
- Invoice-specific WordPress nonces for state-changing requests.
- Input sanitization and contextual output escaping.
- Server-side WooCommerce price lookup and saved price snapshots.
- Stored amount and Authority matching during verification.
- Callback validation before any invoice is marked as paid.
- Payment confirmation only after a successful ZarinPal Verify response.
- Verification lock to reduce duplicate concurrent processing.
- Redacted logging disabled by default.

## Requirements

- WordPress 6.3 or later
- PHP 7.4 or later
- A ZarinPal Merchant ID
- WooCommerce only when product-based invoices are needed

## Installation

### WordPress dashboard

1. Download `tahanoa-invoice-links-for-zarinpal-1.5.9.zip`.
2. Open **Plugins → Add New → Upload Plugin**.
3. Upload the ZIP and activate the plugin.
4. Create a published WordPress page and add `[ezinv_invoice]`.
5. Open **Invoices → Settings**, enter the Merchant ID, and select that page.

### Manual installation

```bash
git clone https://github.com/Tahanoa/easy-zarinpal-invoice.git
```

Copy the `tahanoa-invoice-links-for-zarinpal` directory to `wp-content/plugins/`, then activate it from the WordPress dashboard.

## Shortcode

```text
[ezinv_invoice]
```

The legacy `[ezi_invoice]` shortcode remains supported for migration compatibility.

## Payment flow

1. The administrator creates an invoice and shares its public link.
2. The customer submits payment from the invoice page.
3. The plugin requests an Authority from ZarinPal using the stored invoice amount.
4. ZarinPal returns the customer to the callback URL.
5. The plugin validates the callback and stored Authority.
6. The payment is marked as paid only after ZarinPal Verify succeeds.

The Inquiry endpoint reports transaction state only; it never verifies a transaction or marks an invoice as paid.

## External service disclosure

Payment operations connect to ZarinPal. Depending on the requested operation, the plugin sends the configured Merchant ID, stored invoice amount, description, callback URL, invoice ID, Authority, and optional customer email/mobile fields required for payment processing.

- [ZarinPal website](https://www.zarinpal.com/)
- [Terms of service](https://www.zarinpal.com/terms)
- [Privacy policy](https://www.zarinpal.com/policy)

The plugin does not send telemetry or analytics to its author.

## Changelog

### 1.5.9

- Renamed the plugin to Tahanoa Invoice Links for ZarinPal.
- Updated the slug, text domain, translation files, and documentation.

### 1.5.8

- Added gateway response-size protection.
- Improved payment-state database error handling.
- Validated documented ZarinPal Inquiry statuses.
- Hardened fixed shipping amount validation.

### 1.5.7

- Improved request sanitization and WordPress.org compatibility.
- Replaced direct WooCommerce SKU SQL lookup with `WP_Query`.
- Added explicit object caching and cache invalidation.
- Improved uninstall handling and Plugin Check compatibility.

## Contributing

Bug reports and pull requests are welcome. For security vulnerabilities, contact the maintainer privately before public disclosure.

## License

GPL-2.0-or-later. See [LICENSE](tahanoa-invoice-links-for-zarinpal/LICENSE).

## Author

[Taha Farzaneh](https://github.com/Tahanoa)
