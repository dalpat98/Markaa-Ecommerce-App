# Markaa Ecommerce App

Markaa is an Kuwait Based Ecommerce Company, Major in selling Skin care Products.
 
 Technologies used in the APP :

- Flutter
- Dart
- Go Sell Tap Payments SDK
- Google cloud

<a href='https://play.google.com/store/apps/details?id=com.app.markaa&hl=en_IN&gl=US'><img alt='Get it on Google Play' src='https://play.google.com/intl/en_us/badges/images/generic/en_badge_web_generic.png' height=80px/></a>

Flutter plugin compatible version of goSellSDK library for both Android and iOS that fully covers payment/authorization/card saving/card tokenization process inside your Android application.

Original SDKS

- Android (https://github.com/Tap-Payments/goSellSDK-Android)
- AndroidX (https://github.com/Tap-Payments/goSellSDK-AndroidX)
- iOS (https://github.com/Tap-Payments/goSellSDK-ios)

## Getting Started

# Table of Contents

---

1. [Requirements](#requirements)
2. [Installation](#installation)
   1. [Installation with pubspec.yaml](#installation_with_pubspec)
3. [Usage](#usage)
   1. [Configure Your App](#configure_your_app)
   2. [Configure SDK Session](#configure_sdk_session)
   3. [Use Tap Pay Button](#tap_pay_button)
   4. [Handle SDK Result](#handle_sdk_result)

<a href="requirements"></a>


### Some Screenshots

<img height="480px" src="https://user-images.githubusercontent.com/49696449/126716478-f111723f-0afe-4ac2-9eea-b40b8810a5ea.png">  <img height="480px" src="https://user-images.githubusercontent.com/49696449/126716483-cf7db309-3ffc-4b1c-9285-78f7ba36e0b0.png">  <img height="480px" src="https://user-images.githubusercontent.com/49696449/126716486-e7b058e1-683a-4b66-971d-ec6b7839617d.png">  <img height="480px" src="https://user-images.githubusercontent.com/49696449/126716489-ddef80d3-f64c-4f5c-bf2b-1a6655e9b89e.png">  <img height="480px" src="https://user-images.githubusercontent.com/49696449/126716492-a4a54643-3534-4944-a184-54cc84de3db6.png">  <img height="480px" src="https://user-images.githubusercontent.com/49696449/126716497-2c0fd14a-e472-46d4-8571-adf99e29a09a.png">  <img height="480px" src="https://user-images.githubusercontent.com/49696449/126716499-be18a6b8-3459-43ea-a7bd-311ce553e52c.png">  <img height="480px" src="https://user-images.githubusercontent.com/49696449/126716502-8eab47c4-cb44-4836-a6ce-4a445f657e8f.png">  <img height="480px" src="https://user-images.githubusercontent.com/49696449/126716505-0a127f6d-0303-4db8-ba23-e9cb33627675.png">  <img height="480px" src="https://user-images.githubusercontent.com/49696449/126716509-2df76d29-935a-4d74-8b37-496da92d76e9.png">  <img height="480px" src="https://user-images.githubusercontent.com/49696449/126716512-1da5eccd-bb8f-4b0f-baf0-d20c4e2316d6.png">

# Requirements

---

To use the SDK the following requirements must be met:

1. **Visual Studio - InteliJ Idea**
2. **Dart 2.7.1** or newer
3. **Flutter: >=1.10.0** or newer
4. **iOS 11** or later
5. **XCode 12** or later

<a name="installation"></a>

# Installation

---

<a name="installation_with_pubspec"></a>

### Include goSellSDK plugin as a dependency in your pubspec.yaml

```dart
 dependencies:
     tap_payment_markaa: ^2.0.3
```

---

<a name="configure_your_app"></a>

## Configure your app

`goSellSDK` should be set up. To set it up, add the following lines of code somewhere in your project and make sure they will be called before any usage of `goSellSDK`.

```dart
/**
 * Configure App. (You must get those keys from tap)
 */
GoSellSdkFlutter.configureApp(
  bundleId: "ANDROIID-PACKAGE-NAME",
  productionSecreteKey: Platform.isAndroid? "Android-Live-KEY" : "iOS-Live-KEY",
  sandBoxsecretKey: Platform.isAndroid?"Android-SANDBOX-KEY" : "iOS-SANDBOX-KEY",
  lang: "en");
```

---

<a name="configure_your_app"></a>
**Configure SDK Session Example**

```dart
Future<void> setupSDKSession() async {
    try {
    GoSellSdkFlutter.sessionConfigurations(
        trxMode: TransactionMode.TOKENIZE_CARD,
        transactionCurrency: "kwd",
        amount: '100',
        customer: Customer(
            customerId: "",
            email: "h@tap.company",
            isdNumber: "965",
            number: "000000",
            firstName: "Haitham",
            middleName: "Mohammad",
            lastName: "Elsheshtawy",
            metaData: null),
        paymentItems: <PaymentItem>[
            PaymentItem(
                name: "item1",
                amountPerUnit: 1,
                quantity: Quantity(value: 1),
                discount: {
                "type": "F",
                "value": 10,
                "maximum_fee": 10,
                "minimum_fee": 1
                },
                description: "Item 1 Apple",
                taxes: [
                Tax(
                    amount: Amount(
                        type: "F",
                        value: 10,
                        minimum_fee: 1,
                        maximum_fee: 10),
                    name: "tax1",
                    description: "tax describtion")
                ],
                totalAmount: 100),
        ],
        // List of taxes
        taxes: [
            Tax(
                amount: Amount(
                    type: "F", value: 10, minimum_fee: 1, maximum_fee: 10),
                name: "tax1",
                description: "tax describtion"),
            Tax(
                amount: Amount(
                    type: "F", value: 10, minimum_fee: 1, maximum_fee: 10),
                name: "tax1",
                description: "tax describtion")
        ],
        // List of shippnig
        shippings: [
            Shipping(
                name: "shipping 1",
                amount: 100,
                description: "shiping description 1"),
            Shipping(
                name: "shipping 2",
                amount: 150,
                description: "shiping description 2")
        ],
        // Post URL
        postURL: "https://tap.company",
        // Payment description
        paymentDescription: "paymentDescription",
        // Payment Metadata
        paymentMetaData: {
            "a": "a meta",
            "b": "b meta",
        },
        // Payment Reference
        paymentReference: Reference(
            acquirer: "acquirer",
            gateway: "gateway",
            payment: "payment",
            track: "track",
            transaction: "trans_910101",
            order: "order_262625"),
        // payment Descriptor
        paymentStatementDescriptor: "paymentStatementDescriptor",
        // Save Card Switch
        isUserAllowedToSaveCard: true,
        // Enable/Disable 3DSecure
        isRequires3DSecure: false,
        // Receipt SMS/Email
        receipt: Receipt(true, false),
        // Authorize Action [Capture - Void]
        authorizeAction: AuthorizeAction(
            type: AuthorizeActionType.CAPTURE, timeInHours: 10),
        // Destinations
        destinations:Destinations(
            amount: 100,
            currency: 'kwd',
            count: 2,
            destinationlist: [
                Destination(
                    id: "",
                    amount: 100,
                    currency: "kwd",
                    description: "des",
                    reference: "ref_121299"),
                Destination(
                    id: "",
                    amount: 100,
                    currency: "kwd",
                    description: "des",
                   reference: "ref_22444444")
            ])
        ,
        // merchant id
        merchantID: "",
        // Allowed cards
        allowedCadTypes: CardType.CREDIT,
        applePayMerchantID: "applePayMerchantID",
        allowsToSaveSameCardMoreThanOnce: false,
        // pass the card holder name to the SDK
        cardHolderName: "Card Holder NAME",
        // disable changing the card holder name by the user
        allowsToEditCardHolderName: false,
        paymentType: PaymentType.ALL,
        sdkMode: SDKMode.Sandbox);
    } on PlatformException {
    }
```

---

<a name="tap_pay_button"></a>
**Use Tap Pay Button**

```dart
Positioned(
    bottom: Platform.isIOS ? 0 : 10,
    left: 18,
    right: 18,
    child: SizedBox(
        height: 45,
        child: RaisedButton(
          color: _buttonColor,
          clipBehavior: Clip.hardEdge,
          shape: RoundedRectangleBorder(
              borderRadius: BorderRadiusDirectional.all(
                  Radius.circular(30))),
          onPressed: startSDK,
          child: Row(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Container(
                  width: 25,
                  height: 25,
                  child: AwesomeLoader(
                    outerColor: Colors.white,
                    innerColor: Colors.white,
                    strokeWidth: 3.0,
                    controller: loaderController,
                  ),
                ),
                Spacer(),
                Text('PAY',
                    style: TextStyle(
                        color: Colors.white, fontSize: 16.0)),
                Spacer(),
                Icon(
                  Icons.lock_outline,
                  color: Colors.white,
                ),
              ]),
        )),
          ),
```

---

<a name="handle_sdk_result"></a>
**Handle SDK Result**

- Start SDK

```dart
   tapSDKResult = await GoSellSdkFlutter.startPaymentSDK;
```

- Hnadle SDK result

```dart
setState(() {
  switch (tapSDKResult['sdk_result']) {
    case "SUCCESS":
      sdkStatus = "SUCCESS";
      handleSDKResult();
      break;
    case "FAILED":
      sdkStatus = "FAILED";
      handleSDKResult();
      break;
    case "SDK_ERROR":
      sdkErrorCode                  = tapSDKResult['sdk_error_code'].toString();
      sdkErrorMessage               = tapSDKResult['sdk_error_message'];
      sdkErrorDescription           = tapSDKResult['sdk_error_description'];
      break;
    case "NOT_IMPLEMENTED":
      sdkStatus = "NOT_IMPLEMENTED";
      break;
  }
});
void handleSDKResult() {
  switch (tapSDKResult['trx_mode']) {
    case "CHARGE":
    case "AUTHORIZE":
    case "SAVE_CARD":
        extractSDKResultKeysAndValues();
        break;
    case "TOKENIZE":
        token :                          =tapSDKResult['token'];
        token_currency                   =tapSDKResult['token_currency'];
        card_first_six                   =tapSDKResult['card_first_six'];
        card_last_four                   =tapSDKResult['card_last_four'];
        card_object                      =tapSDKResult['card_object'];
        card_exp_month                   =tapSDKResult['card_exp_month'];
        card_exp_year                    =tapSDKResult['card_exp_year'];
        break;
  }
}
void extractSDKResultKeysAndValues() {
    id                             = tapSDKResult['charge_id'];
    description                    = tapSDKResult['description'];
    message                        = tapSDKResult['message'];
    card_first_six                 = tapSDKResult['card_first_six'];
    card_last_four                 = tapSDKResult['card_last_four'];
    card_object                    = tapSDKResult['card_object'];
    card_brand                     = tapSDKResult['card_brand'];
    card_exp_month                 = tapSDKResult['card_exp_month'];
    card_exp_year                  = tapSDKResult['card_exp_year'];
    acquirer_id                    = tapSDKResult['acquirer_id'];
    acquirer_response_code         = tapSDKResult['acquirer_response_code'];
    acquirer_response_message      = tapSDKResult['acquirer_response_message'];
    source_id                      = tapSDKResult['source_id'];
    source_channel                 = tapSDKResult['source_channel'];
    source_object                  = tapSDKResult['source_object'];
    source_payment_type            = tapSDKResult['source_payment_type'];
    responseID                     = tapSDKResult['charge_id'];
}
```

---

### The stack & building from source

The project is currently built using the latest Flutter Master, with Dart 2 enabled.

To build the project, ensure that you have a recent version of the Flutter SDK installed. Then either run `flutter run` in the project root or use your IDE of choice.

### :heart: Found this project useful?

If you found this project useful, then please consider giving it a :star: on Github and sharing it with your friends via social media.


## Getting Started
- Clone or download
- Build and Run

# Pull Requests

I welcome and encourage all pull requests. It usually will take me within 24-48 hours to respond to any issue or request. Here are some basic rules to follow to ensure timely addition of your request:

1.  Match the document style as closely as possible.
2.  Please keep PR titles easy to read and descriptive of changes, this will make them easier to merge :)
3.  Pull requests _must_ be made against `master` branch for this particular repository.
4.  Make sure you follow the set standard as all other projects in this repo do
5.  Have fun!


        
<p align="center">
  <b><i>Let's connect! Find me on the web.</i></b>

[<img height="30" src="https://img.shields.io/badge/twitter-%231DA1F2.svg?&style=for-the-badge&logo=twitter&logoColor=white" />][twitter]
[<img height="30" src="https://img.shields.io/badge/linkedin-blue.svg?&style=for-the-badge&logo=linkedin&logoColor=white" />][linkedin]
[<img height="30" src = "https://img.shields.io/badge/Facebook-036be4.svg?&style=for-the-badge&logo=facebook&logoColor=white">][Facebook]
[<img height="30" src = "https://img.shields.io/badge/instagram-c14438?&style=for-the-badge&logo=instagram&logoColor=white">][instagram]
<br />
<hr />

[twitter]: https://twitter.com/DalpatDc
[linkedin]: https://www.linkedin.com/in/dalpat-i-b5b451166/
[instagram]: https://www.instagram.com/dalpat_chaudhary__/
[Facebook]: https://www.facebook.com/dalpatchaudhary.blogspot.in/

If you have any Queries or Suggestions, feel free to reach out to me.
<h3 align="center">Show some &nbsp;❤️&nbsp; by starring some of the repositories!</h3>

