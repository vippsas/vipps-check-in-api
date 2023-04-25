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

<!-- START_COMMENT -->

ℹ️ Please use the website:
[Vipps MobilePay Technical Documentation](https://developer.vippsmobilepay.com/docs/APIs/check-in-api).

<!-- END_COMMENT -->

## Before you begin

This document covers the quick steps for getting started with the Vipps Check-in API.
You must have already signed up as a organisation with Vipps and have your test credentials from the merchant portal, as described in the
[Vipps Getting Started guide](https://developer.vippsmobilepay.com/docs/vipps-developers/getting-started).

### HTTP headers

We strongly recommend using these standard
[HTTP headers](https://developer.vippsmobilepay.com/docs/vipps-developers/common-topics/http-headers)
for all requests.

### Authentication

All API requests are authenticated with an access token and an API subscription key.
See
[Get an access token](https://developer.vippsmobilepay.com/docs/APIs/access-token-api#get-an-access-token)
in the Getting started guide, for details.

## Loyalty check-in

The *loyalty check-in* is a way of showing the user their membership status. This is used to keep the customers in the app, while also informing them if they are member or not.

Here is how they will look based on `isMember`. The merchants logo will also show here.
![Loyalty Flow](images/loyalty_check_in.png)

## API example

[`POST:point-of-sale/v1/loyalty-check-in`](https://developer.vippsmobilepay.com/api/check-in#tag/point-of-sale/operation/initiateLoyaltyCheckIn)

Headers:

```json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1Ni <snip>
Ocp-Apim-Subscription-Key: 0f14ebcab0ec4b29ae0cb90d91b4a84a
Accept: image/png
Merchant-Serial-Number: 123456
Vipps-System-Name: acme
Vipps-System-Version: 3.1.2
Vipps-System-Plugin-Name: acme-pos
Vipps-System-Plugin-Version 4.5.6
```

### The request body

| Parameter            | Type      | Required | Description                                                          |
| -------------------- | --------- | -------- | -------------------------------------------------------------------- |
| `phoneNumber`        | `string`  | Y        | The phone number of the end user, fetched via their personal QR-code |
| `isMember`           | `boolean` | Y        | This boolean will trigger different user flows in the app to show the the user if they are already enrolled in the loyalty program or not. If this value is `true` it means they are a member and already enrolled. |

Body:

```json
{
  "phoneNumber": "4791234567",
  "isMember": false
}
```

The response will simply be a GUID, which is a reference that may be used for debugging.

## Merchant enrollment

If merchants want a special name for their customer club, contact Vipps MobilePay Payment Experience team and we can add the name manually. If no name is set, we will use the company name in addition to "customer club".
