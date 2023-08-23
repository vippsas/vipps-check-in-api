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

This document covers the quick steps for getting started with the ePayment API.
You must have already signed up as an organization with Vipps MobilePay.

**Important:** The examples use standard example values that you must change to
use *your* values. This includes API keys, HTTP headers, reference, etc.

## Your first check-in notification

Be aware that these are running on the production server, <https://api.vipps.no>.

### Step 1 - Setup

<Tabs
defaultValue="curl"
groupId="sdk-choice"
values={[
{label: 'curl', value: 'curl'},
{label: 'Postman', value: 'postman'},
]}>
<TabItem value="postman">

**Please note:** Postman is discontinuing their offline version. Use only your test keys and delete them after testing. Ensure that your company allows for cloud use before continuing.

If you wish to use Postman, import the following files:

* [Check-in API Postman collection](/tools/vipps-check-in-api-postman-collection.json)
* [Global Postman environment](https://github.com/vippsas/vipps-developers/blob/master/tools/vipps-api-global-postman-environment.json)

In Postman, tweak the environment with your own values (see
[API keys](https://developer.vippsmobilepay.com/docs/common-topics/api-keys/)):

* `client_id` - Merchant key required for getting the access token.
* `client_secret` - Merchant key required for getting the access token.
* `Ocp-Apim-Subscription-Key` - The subscription key for making API requests.
* `merchantSerialNumber` - The unique ID for your sales unit.
* `internationalMobileNumber` - The MSISDN for your Vipps profile.
* `base_url_production` - Set to: `https://api.vipps.no`.

</TabItem>
<TabItem value="curl">

No setup needed :)

</TabItem>
</Tabs>

### Step 2 - Authentication

For all the following, you will need an `access_token` from the
[Access token API](https://developer.vippsmobilepay.com/docs/APIs/access-token-api):
[`POST:/accesstoken/get`](https://developer.vippsmobilepay.com/api/access-token#tag/Authorization-Service/operation/fetchAuthorizationTokenUsingPost).
This provides you with access to the API.

<Tabs
defaultValue="curl"
groupId="sdk-choice"
values={[
{label: 'curl', value: 'curl'},
{label: 'Postman', value: 'postman'},
]}>
<TabItem value="postman">

```bash
Send request Get Access Token
```

</TabItem>
<TabItem value="curl">

```bash
curl https://api.vipps.no/accessToken/get \
-H "client_id: YOUR-CLIENT-ID" \
-H "client_secret: YOUR-CLIENT-SECRET" \
-H "Ocp-Apim-Subscription-Key: YOUR-SUBSCRIPTION-KEY" \
-H "Merchant-Serial-Number: 123456" \
-H "Vipps-System-Name: acme" \
-H "Vipps-System-Version: 3.1.2" \
-X POST \
--data ''
```

</TabItem>
</Tabs>

The property `access_token` should be used for all other API requests in the `Authorization` header as the Bearer token.

### Step 3 - Open your Vipps app

Open your Vipps app to be able to see the notification.

### Step 4 - Your Check-in notification

Initiate a notification with: [`POST:point-of-sale/v1/loyalty-check-in`](https://developer.vippsmobilepay.com/api/check-in#tag/point-of-sale/operation/initiateLoyaltyCheckIn).
When your mobile number
is provided in `phoneNumber`, it will be pre-filled in the form.

<Tabs
defaultValue="curl"
groupId="sdk-choice"
values={[
{label: 'curl', value: 'curl'},
{label: 'Postman', value: 'postman'},
]}>
<TabItem value="postman">

```bash
Send request Loyalty check-in
```

</TabItem>
<TabItem value="curl">

```bash
curl --location 'https://apitest.vipps.no/point-of-sale/v1/loyalty-check-in' \
-H 'Content-Type: application/json' \
-H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1Ni <truncated>" \
-H "Ocp-Apim-Subscription-Key: 0f14ebcab0ec4b29ae0cb90d91b4a84a" \
-H "Merchant-Serial-Number: 123456" \
-H "Vipps-System-Name: acme" \
-H "Vipps-System-Version: 3.1.2" \
-H "Vipps-System-Plugin-Name: acme-webshop" \
-H "Vipps-System-Plugin-Version: 4.5.6" \
-X POST \
-d '{
  "phoneNumber": 4796574209,
  "isMember": true
}'
```

</TabItem>
</Tabs>

The check-in screen should show.

**Please note:** If you use `"isMember": false`, nothing will happen. This is the expected behavior.

## Next Steps

See:

* [In-store payments with customer club](https://developer.vippsmobilepay.com/docs/solutions/loyalty-in-pos) for a full flow with examples.
* [Check-in API guide](vipps-check-in-api.md) to read about the concepts and details.