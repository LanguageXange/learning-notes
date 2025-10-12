## Apple Pay Glossary

- PSP ( Payment Service Provider ) https://developer.apple.com/apple-pay/payment-platforms/
- PNO ( Payment Network Operator ) e.g. Visa, MasterCard
- CSR (Certificate Signing Request )
- Apple Pay payment object ; Apple Pay Session
- Merchant Validation
- Merchant Server
- Apple Server



## Links

- https://developer.apple.com/documentation/technotes/tn3103-apple-pay-on-the-web-troubleshooting-guide
- https://developer.apple.com/apple-pay/Apple-Pay-Merchant-Integration-Guide.pdf ( page 23 includes API diagram )
- https://developer.apple.com/documentation/applepayontheweb ( for Web )
- https://developer.apple.com/apple-pay/payment-platforms/
- https://applepaydemo.apple.com/ Apple pay demo
- https://support.apple.com/zh-tw/102897  Apple Pay 特約銀行
- [apple-pay-申請流程手把手教學](https://michaelrevlis.medium.com/apple-pay-%E7%94%B3%E8%AB%8B%E6%B5%81%E7%A8%8B%E6%89%8B%E6%8A%8A%E6%89%8B%E6%95%99%E5%AD%B8-3166dad321b4)
( 2022 Medium 文章 although it’s for iOS development )

## Steps ( based on above medium article )

1. Apple Developer Account
2. Register Merchant ID
3. Generate CSR ( Certificate Signing Request ) see KeyChain Access App
4. Apply Apple Pay Payment Certificate ( using CSR from step 3 )  ( apple_pay.cer file )

## API - Payment Request vs Apple Pay API

- Choosing an API  https://developer.apple.com/documentation/applepayontheweb/choosing-an-api-for-implementing-apple-pay-on-your-website
- Payment Request API
https://developer.apple.com/documentation/ApplePayontheWeb/payment-request-api
- Apple Pay JS API 
https://developer.apple.com/documentation/applepayontheweb/apple-pay-js-api


## API Diagram ( PDF integration guide )

https://developer.apple.com/apple-pay/Apple-Pay-Merchant-Integration-Guide.pdf
