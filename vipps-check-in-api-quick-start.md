<!-- START_METADATA
---
title: Quick start for the Check-in API
sidebar_label: Quick start
sidebar_position: 20
description: Quick steps for getting started with the Check-in API.
toc_min_heading_level: 2
toc_max_heading_level: 5
pagination_next: null
pagination_prev: null
---

import ApiSchema from '@theme/ApiSchema';
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

END_METADATA -->

# Quick start

## Before you begin

The provided example values in this guide must be changed with the values for your sales unit and user.
This applies for API keys, HTTP headers, reference, phone number, etc.

## Your first check-in notification

Be aware that these are running on the production server, [https://api.vipps.no](https://api.vipps.no).

### Step 1 - Setup

You must have already signed up as an organization with Vipps MobilePay and have
your test credentials from the merchant portal.

You will need the following values, as described in the
[Getting started guide](https://developer.vippsmobilepay.com/docs/getting-started):

* `client_id` - Client_id for a test sales unit.
* `client_secret` - Client_id for a test sales unit.
* `Ocp-Apim-Subscription-Key` - The subscription key for a test sales unit.
* `Merchant-Serial-Number` - The unique ID for a test sales unit.
* `internationalMobileNumber` - The MSISDN for your Vipps MobilePay profile.

### Step 2 - Authentication

For all the following, you will need an `access_token` from the
[Access token API](https://developer.vippsmobilepay.com/docs/APIs/access-token-api):
[`POST:/accesstoken/get`](https://developer.vippsmobilepay.com/api/access-token#tag/Authorization-Service/operation/fetchAuthorizationTokenUsingPost).
This provides you with access to the API.

```bash
curl https://api.vipps.no/accessToken/get \
-H "client_id: YOUR-CLIENT-ID" \
-H "client_secret: YOUR-CLIENT-SECRET" \
-H "Ocp-Apim-Subscription-Key: YOUR-SUBSCRIPTION-KEY" \
-H "Merchant-Serial-Number: YOUR-MSN" \
-H "Vipps-System-Name: acme" \
-H "Vipps-System-Version: 3.1.2" \
-X POST \
--data ''
```


The property `access_token` should be used for all other API requests in the `Authorization` header as the Bearer token.

### Step 3 - Open your Vipps app

Open your Vipps app to be able to see the notification.

### Step 4 - Your Check-in notification

Initiate a notification with: [`POST:/point-of-sale/v1/loyalty-check-in`](https://developer.vippsmobilepay.com/api/check-in#tag/point-of-sale/operation/initiateLoyaltyCheckIn).
When your mobile number
is provided in `phoneNumber`, it will be prefilled in the form.

```bash
curl --location 'https://apitest.vipps.no/point-of-sale/v1/loyalty-check-in' \
-H 'Content-Type: application/json' \
-H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1Ni <truncated>" \
-H "Ocp-Apim-Subscription-Key: 0f14ebcab0ec4b29ae0cb90d91b4a84a" \
-H "Merchant-Serial-Number: YOUR-MSN" \
-H "Vipps-System-Name: acme" \
-H "Vipps-System-Version: 3.1.2" \
-H "Vipps-System-Plugin-Name: acme-webshop" \
-H "Vipps-System-Plugin-Version: 4.5.6" \
-X POST \
-d '{
  "phoneNumber": 4712345678,
  "isMember": true
}'
```

The check-in screen should show.

**Please note:** If you use `"isMember": false`, nothing will happen. This is the expected behavior.

## Next Steps

See [Check-in API guide](vipps-check-in-api.md) to read about the concepts and details.
