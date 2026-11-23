# Receipt

A static, client-side receipt page. When `receiptData` is provided, every
visible receipt string comes from that one URL parameter as a URL-encoded JSON
array. No form or server is required. Each page visit adds a fresh `timestamp`
query parameter to avoid reusing a cached page URL.

## URL format

The JSON array contains 17 rows in this order:

| Index | Contents |
| --- | --- |
| 0 | notice, watermark, custom details |
| 1 | merchant name, Arabic name, location |
| 2 | date, time |
| 3-4 | two identifier rows |
| 5-6 | payment method and transaction type rows |
| 7 | masked card number, expiry |
| 8 | Arabic label/amount, English label/amount |
| 9-10 | Arabic/English status and verification rows |
| 11-13 | approval code/label, English label/code, date/time |
| 14 | six Arabic/English footer strings |
| 15-16 | two technical rows of three strings |

Example:

```js
const receiptData = [
  ["DEMO · NOT PAYMENT PROOF", "DEMO", ""],
  ["Merchant", "اسم التاجر", "Location"],
  ["23/11/2026", "13:41:38"],
  ["Transaction ID", "Order ID"],
  ["Terminal", "Reference"],
  ["mada", "مدى"],
  ["PURCHASE", "شراء"],
  ["0000 **** **** 0000", "03/29"],
  ["مبلغ الشراء", "﷼١٠٠.٠٠", "PURCHASE AMOUNT", "SAR 100.00"],
  ["مقبولة", "APPROVED"],
  ["لا يتطلب التحقق", "NO VERIFICATION REQUIRED"],
  ["٢١٧١٢٧", "رمز الموافقة"],
  ["Approval Code", "217127"],
  ["23/11/2026", "13:41:38"],
  [
    "شكرا لاستخدامك مدى", "THANK YOU FOR USING mada",
    "يرجى الاحتفاظ بالإيصال", "PLEASE RETAIN RECEIPT",
    "** نسخة العميل **", "** CUSTOMER COPY **"
  ],
  ["CONTACTLESS 000", "A0000002282010", "0000000000"],
  ["0000 80 420300", "410859D733A8DDD2", "03"]
];

const url = new URL("https://edfapay.github.io/edfapay-receipt-generator/");
url.searchParams.set("receiptData", JSON.stringify(receiptData));
console.log(url.href);
```

`URLSearchParams` encodes the JSON array. The page validates all 17 rows
and displays an error for invalid or incomplete data. Earlier individual
parameters remain supported as a compatibility fallback.

**Demo only:** the receipt does not verify or process payments.

## GitHub Pages

The workflow in `.github/workflows/pages.yml` publishes the repository root to
GitHub Pages whenever changes are pushed to `main`. In repository settings,
select **Pages → Build and deployment → Source → GitHub Actions**. The site is
available at `https://edfapay.github.io/edfapay-receipt-generator/`.
