<!-- START_METADATA
---
draft: true
---
END_METADATA -->

# How it works

💥 DRAFT! Unfinished work in progress. API specification changes are still coming. 💥

## Step 1: Scan the QR code

The flow begins with the customer presenting their QR code to the merchant. This can happen two ways:

* Customer-facing scanner. The store will have a permanent customer-facing scanner and customers can scan their QR code at any time.
* The QR code is scanned by the cashier using a wired scanner. This could happen while the cashier is scanning wares or right before the payment.

![Loyalty Flow](images/pos_step_1.png)

## Step 2: Check membership

Check the customer's membership status by using the mobile number you received in the last step.

Automatically trigger a Vipps Check-In to inform the customer whether or not they are a member of your loyalty program. This will help them through the payment process.

![Loyalty Flow](images/pos_step_2.png)


  


<!-- Table of contents -->

<!-- Postman collection -->

## The API
💥 DRAFT! Unfinished work in progress. API specification changes are still coming. 💥  
  
Use this API to open a waiting screen on the endusers phone. The waiting screen can be used to enroll customers into your customer loyalty program, if your system also supports vipps login.

### Before you start
As this is an early access API, we need to enroll your sales unit. To enroll we need you to provide both a subtitle in norwegian and english. The subtitle will be shown under the title on the waiting screen. This is to tailor the waiting screen for your customers, so they can read about the benefits or cool features of your loyalty program. Please contact either your vipps sales representative, partner or send an email to our integration team as described [here](https://vippsas.github.io/vipps-developer-docs/docs/vipps-developers/contact#what-to-include-in-the-email).


### The request headers
| Key            | Value     | Description                                                                   |
| -------------------- | -------- |  ----------------------------------------------------------------------------- |
| `Authorization`             | `Bearer <TOKEN>` | The access token for the API                      |
| `Ocp-Apim-Subscription-Key`      | `YOUR-SUBSCRIPTION-KEY` |   The API-key from the Vipps portal                        |
| `Merchant-Serial-Number`          | `YOUR-MERCHANT-ACCOUNT-NUMBER` |  The merchant serial number for the sale unit                                          |

### The request body
| Parameter            | Type     | Required | Description                                                                   |
| -------------------- | -------- | -------- | ----------------------------------------------------------------------------- |
| `phoneNumber`             | `string` | Y        | The phone number of the enduser, fetched via their personal QR-code                      |
| `loyaltyProgramName`      | `string` | Y        | The name of the loyalty program. This will be shown to the enduser on the waiting screen.                        |
| `isMember`          | `boolean` | Y        | This boolean will trigger different userflows in the app, to show them if they are already enrolled in the loayalty program or not. If this value is `true` it means they are a member, and already enrolled.                                          |
