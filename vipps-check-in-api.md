<!-- START_METADATA
---
title: Check-in API guide
sidebar_label: API guide
sidebar_position: 30
description: Find technical details about integrating with the Check-in API.
pagination_prev: Null
pagination_next: Null
---
END_METADATA -->

# Check-in API

The Check-in API is an interface to use in the Point Of Sale (POS) context for communicating with the customers while they are waiting for a process to be completed.

API version: 1.0.0

## The check-in screen

The check-in screen is a way of showing the user their membership status. As per now, intended app behavior is to only show the check-in screen when the user is a member. This is used to keep the customers in the app, while also informing them that they are a member.

**NB:** The check-in screen will only appear if the user has the app open.

Here is how it will look for the user. The merchant's logo will also show here.
![Loyalty Flow](images/loyalty_check_in_1.png)

Send the
[`POST:point-of-sale/v1/loyalty-check-in`](https://developer.vippsmobilepay.com/api/check-in#tag/point-of-sale/operation/initiateLoyaltyCheckIn)
request to show the check-in screen in the user's Vipps app.

Headers:

```json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1Ni <snip>
Ocp-Apim-Subscription-Key: 0f14ebcab0ec4b29ae0cb90d91b4a84a
Accept: image/png
Merchant-Serial-Number: 123456
Vipps-System-Name: Acme Commerce
Vipps-System-Version: 3.1.2
Vipps-System-Plugin-Name: acme-pos
Vipps-System-Plugin-Version 4.5.6
```

The request body:

| Parameter            | Type      | Required | Description                                                          |
| -------------------- | --------- | -------- | -------------------------------------------------------------------- |
| `phoneNumber`        | `string`  | Y        | The phone number of the end user, fetched via their personal QR-code |
| `isMember`           | `boolean` | Y        | This boolean will determine the user flow in the app to show whether the user is enrolled in the loyalty program or not. If this value is `true`, they are a member and already enrolled, and the check-in screen will show.  If the value is `false`, nothing will be shown on the screen. |

Body:

```json
{
  "phoneNumber": "4791234567",
  "isMember": true
}
```

The response will simply be a GUID, which is a reference that may be used for debugging.

## Merchant enrollment

If merchants want a special name for their customer club, [contact us](https://developer.vippsmobilepay.com/docs/contact/), and we can add the name manually.
If no name is set, we will use the company name in addition to "customer club".
