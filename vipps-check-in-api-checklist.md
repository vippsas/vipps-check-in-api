<!-- START_METADATA
---
title: Check-in API checklist
sidebar_label: Checklist
sidebar_position: 40
description: Checklist for full integration with the Check-in API.
pagination_next: null
pagination_prev: null
draft: false
---
END_METADATA -->

# Checklist

## Endpoints to integrate

Integrate the [API endpoint](https://developer.vippsmobilepay.com/api/check-in/). For examples of requests and responses, see the [Postman collection](/tools/vipps-check-in-api-postman-collection.json) and [environment](https://github.com/vippsas/vipps-developers/blob/master/tools/vipps-api-global-postman-environment.json).

| Endpoint | Comment |
|-----|-----------|
|     Initiate check-in session | [`POST:/point-of-sale/v1/loyalty-check-in`](https://developer.vippsmobilepay.com/api/check-in/#tag/Loyalty-check-in/operation/initiateLoyaltyCheckIn) |

## Quality assurance

| Action | Comment |
|-----------------------|-----------|
|     Handle responses | Make sure to handle the response from the check in session.|
|     Handle errors    | Make sure to log and handle all errors. All integrations should display errors in a way that the users (customers and merchant employees/administrators) can see and understand them.|
|     Include Vipps HTTP Headers      | Send the [HTTP headers](https://developer.vippsmobilepay.com/docs/common-topics/http-headers) in all API requests for better tracking and troubleshooting (mandatory for partners and platforms, who must send these headers as part of the checklist approval). |

## Avoid integration pitfalls

| Action                       | Comment |
|------------------------------|-----------|
|     Follow design guidelines | The Vipps MobilePay branding must be according to the [design guidelines](https://developer.vippsmobilepay.com/docs/design-guidelines).|
|     Educate customer support | Make sure your customer service, etc. has all the tools and information they need available in *your* system, through the APIs listed in the first item in this checklist. Ensure that they do not need to visit [portal.vipps.no](https://portal.vipps.no) for normal work. |
