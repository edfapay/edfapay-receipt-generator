# Receipt Generator

A free, static receipt preview and print page. It runs in the browser and can be
hosted on GitHub Pages without a server or build step.

## Use

Open the published page and fill in the form, or add query parameters directly:

```text
https://edfapay.github.io/edfapay-receipt-generator/?merchant=Example%20Store&amount=49.99&currency=USD&transaction_id=TXN-12345&date=2026-01-31%2014%3A30&status=Demo&payment_method=Card&order_id=ORDER-123&customer=Alex%20Example&description=Sample%20item
```

Supported parameters:

| Parameter | Aliases |
| --- | --- |
| `merchant` | `merchant_name` |
| `amount` | `total` |
| `currency` | |
| `transaction_id` | `transactionId`, `txn_id` |
| `date` | `datetime`, `created_at` |
| `status` | |
| `payment_method` | `method` |
| `order_id` | `orderId` |
| `customer` | `customer_name` |
| `description` | `item` |

Use the form to generate a URL with the current values, and use **Print receipt**
to print or save the preview as a PDF. Query-string values are encoded by the
browser when the form is submitted.

**This is a demo receipt generator.** Receipts are visibly marked “DEMO / NOT
PAYMENT PROOF”; the page does not process payments or verify transactions.

## GitHub Pages

The workflow in `.github/workflows/pages.yml` publishes the repository root to
GitHub Pages whenever changes are pushed to `main`. In the repository settings,
set **Pages → Build and deployment → Source** to **GitHub Actions**. The site
will be available at `https://edfapay.github.io/edfapay-receipt-generator/`.