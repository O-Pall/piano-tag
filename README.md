# Piano Analytics GTM Server Template

A Server-side GTM template that converts standard GA4 e-commerce events into Piano Analytics events to simplify your implementation.

## 📋 Supported Events

| GA4 Event         | Piano Events                                              | Native for Piano |
|-------------------|-----------------------------------------------------------|------------------|
| page_view         | `page.display`                                            | ✅                |
| view_item         | `product.page_display`                                    | ✅                |
| view_item_list    | `product.display`                                         | ✅                |
| select_item       | `product.select`                                          | ❌                |
| search            | `internal_search_result.display`                          | ✅                |
| add_to_cart       | `cart.creation` / `cart.update` + `product.add_to_cart`   | ✅                |
| remove_from_cart  | `cart.update` + `product.remove_from_cart`                | ✅                |
| view_cart         | `cart.display` (+ `cart.update` if desynchronized)        | ✅                |
| begin_checkout    | `cart.begin_checkout` (+ `cart.update` if desynchronized) | ❌                |
| add_shipping_info | `cart.delivery` (+ `cart.update` if desynchronized)       | ✅                |
| add_payment_info  | `cart.payment` (+ `cart.update` if desynchronized)        | ✅                |
| purchase          | `transaction.confirmation` + `product.purchased`          | ✅                |

Other events won't be renamed.
Standard GA4 parameters will still be mapped to Piano.

## 🍪 Used cookies

| Category   | Description                                                                                                                                                    |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `_pa_cart` | • Persist the cart between pages and visits.<br>• Emission of `cart.update` events in case of desynchronization with Website<br>• Persistance : `30 days`.<br> |
| `_pcid`    | • Identify users (Standard UUID)<br>• Duration : 395 days<br>                                                                                                  |

## 🛒 Product List

Choose whether you want an automatic conversion from GA4 -> Piano or provide a fully customized Piano ready product list.

- **GA4** : [official documentation](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?hl=fr&client_type=gtag).
- **Piano** : [official documentation](https://developers.atinternet-solutions.com/piano-analytics/data-collection/how-to-send-events/sales-insights).

## 💚 Shopify specific

Compatibility with Shopify (Checkout extensibility) is provided.<br>
Requires you to input a User ID (for both logged in and logged out users).

## ⚙️ Logic

| Step | Process                                            |
|------|----------------------------------------------------|
| 1️⃣  | **Event Reception** → Reading data & cookies       |
| 2️⃣  | **Format Detection** → Data normalization          |
| 3️⃣  | **Specific Processing** → By event type            |
| 4️⃣  | **Consistency Check** → Cookie vs event comparison |
| 5️⃣  | **Enrichment** → Adding configured parameters      |
| 6️⃣  | **Transmission** → Sending to Piano API            |

## 🛠 Troubleshooting

| Issue                 | Resolution                                    |
|-----------------------|-----------------------------------------------|
| **Data Loss**         | Check the consistency of incoming data format |
| **Duplicates**        | Validate the uniqueness of sent events        |
| **Desynchronization** | Monitor unexpected `cart.update` events       |

## 🔒 Disclaimer

Created by [Addingwell](https://www.addingwell.com).  
Maintained by Addingwell & the community.

Ensure you understand how the template works.

If your incoming data does not correspond to a regular Google Analytics 4 format, you might face issues during the `GA4 → Piano` conversion.

---

This template is designed to simplify the integration between Google Analytics 4 and Piano Analytics while automatically managing the complexities of e-commerce tracking.
