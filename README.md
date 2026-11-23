# Receipt

A static, client-side receipt page. When `receiptData` is provided, every
visible receipt string comes from that one URL parameter as a URL-encoded JSON
object. No form or server is required.

## URL format

The JSON object uses these fields:

| Field | Shape |
| --- | --- |
| `notice`, `watermark`, `customDetails` | String |
| `header` | Three strings: merchant name, Arabic name, location |
| `dateTime` | Two strings: date, time |
| `identifiers` | Two rows of two strings |
| `payment` | Two rows of two strings (for example `mada` / `مدى`, `PURCHASE` / `شراء`) |
| `card` | Two strings: masked number, expiry |
| `amount` | Four strings: Arabic label, Arabic amount, English label, English amount |
| `status`, `verification` | Two strings each: Arabic, English |
| `approval` | Three rows of two strings: Arabic code/label, English label/code, date/time |
| `footer` | Six strings: Arabic and English thank-you, retention, and copy text |
| `technical` | Two rows of three strings |

Example:

```js
const receiptData = {
  notice: "DEMO · NOT PAYMENT PROOF",
  watermark: "DEMO",
  header: ["Merchant", "اسم التاجر", "Location"],
  dateTime: ["23/11/2026", "13:41:38"],
  identifiers: [["Transaction ID", "Order ID"], ["Terminal", "Reference"]],
  payment: [["mada", "مدى"], ["PURCHASE", "شراء"]],
  card: ["0000 **** **** 0000", "03/29"],
  amount: ["مبلغ الشراء", "﷼١٠٠.٠٠", "PURCHASE AMOUNT", "SAR 100.00"],
  status: ["مقبولة", "APPROVED"],
  verification: ["لا يتطلب التحقق", "NO VERIFICATION REQUIRED"],
  approval: [["٢١٧١٢٧", "رمز الموافقة"], ["Approval Code", "217127"], ["23/11/2026", "13:41:38"]],
  footer: [
    "شكرا لاستخدامك مدى", "THANK YOU FOR USING mada",
    "يرجى الاحتفاظ بالإيصال", "PLEASE RETAIN RECEIPT",
    "** نسخة العميل **", "** CUSTOMER COPY **"
  ],
  technical: [
    ["CONTACTLESS 000", "A0000002282010", "0000000000"],
    ["0000 80 420300", "410859D733A8DDD2", "03"]
  ],
  customDetails: ""
};

const url = new URL("https://edfapay.github.io/edfapay-receipt-generator/");
url.searchParams.set("receiptData", JSON.stringify(receiptData));
console.log(url.href);
```

`URLSearchParams` encodes the JSON value. The page validates the complete
object and displays an error for invalid or incomplete data. Earlier individual
parameters remain supported as a compatibility fallback.

**Demo only:** the receipt does not verify or process payments.

## GitHub Pages

The workflow in `.github/workflows/pages.yml` publishes the repository root to
GitHub Pages whenever changes are pushed to `main`. In repository settings,
select **Pages → Build and deployment → Source → GitHub Actions**. The site is
available at `https://edfapay.github.io/edfapay-receipt-generator/`.
