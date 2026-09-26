# Panencia · Pedidos

The order book for Panencia, a small sourdough bakery. A customer writes on WhatsApp, you turn the message into an order, send them a clean summary with the total, and later mark it paid and delivered. The order itself is the sales record, so there's nothing to reconcile at the end of the week.

> The interface is in Spanish.

## Tabs

| Tab | What it's for |
|---|---|
| **Nuevo** | Pick the customer, tap products, set the delivery day, shipping or discount, and whether it's already paid. Or paste the customer's message ("2 hogazas de hierbas y un apple pie para el sábado") and it fills the order for you to review. Saving produces the message for the customer, with Copy and Open WhatsApp buttons. |
| **Pedidos** | The week's orders grouped by delivery day. Mark them paid (transfer or cash) or delivered, resend the message, edit or delete. "Todo lo que me deben" lists every unpaid order. |
| **Semana** | Sold, collected, still owed, estimated profit, the bake list (pieces per product per delivery day) and the last eight weeks. |
| **Menú** | Prices, costs, the ways people ask for each product, what's on sale, and the payment note appended to every order message. |

Weeks run Monday to Sunday and an order counts in the week of its delivery day.

## Where the data lives

This copy keeps everything in your browser (`localStorage`), starting from Panencia's menu. Nobody else sees it, and it doesn't sync between devices.

The real one runs as a Claude artifact with a private shared database, so the bakery sees the same orders from their phones and Claude can read or load sales from chat. The same file works in both places: inside Claude it uses the `db` capability, anywhere else it falls back to the browser.

## Source

This file is generated from `app/pedidos.html` in [carlosglc/panencia_sales_system](https://github.com/carlosglc/panencia_sales_system) with `python3 scripts/standalone.py <output>`. Edit it there, not here.
