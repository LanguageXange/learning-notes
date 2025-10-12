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

- Apple Pay for physical goods versus In-App Purchase for virtual goods
- https://developer.apple.com/apple-pay/acceptable-use-guidelines-for-websites/
- https://developer.apple.com/design/human-interface-guidelines/apple-pay#Using-Apple-Pay-buttons ( Design Guideline )

## Payment Flow (page 5)

Apple Pay uses device-specific tokenized credit or debit card credentials (DPAN) in place of a Payment Account Number (PAN). When users authenticate the payment using their biometric data or passcode, the tokenized card data is returned to your app or website. This token can then be passed to your Payment Service Provider (PSP) to process as you would for a typical online credit or debit card payment

Customer → payment data sent to Apple Server (encrypt data) → `onpaymentauthorized` → Website → Merchant Server → PSP ( decrypt payment obj ) → Acquirer (收單行)→ Payment Network ( de-tokenizes payment data ) → Issuer ( Authorizes payment ) → return Authorization response 

## Setting up your server

https://developer.apple.com/documentation/applepayontheweb/setting-up-your-server 

Production domain

[apple-pay-gateway.apple.com](http://apple-pay-gateway.apple.com/) (Global) 

Sandbox domain

[apple-pay-gateway-cert.apple.com](http://apple-pay-gateway-cert.apple.com/) (Global)

## Configure Apple Pay

1. Apple Developer Account
2. Create a Merchant ID ( never expires )
3. Create Payment Processing Certificate ( renew every 25 months ) → for encrypting Apple pay transaction data
    1. generate your own Certificate Signing Request ( CSR ) 
    2. PSP will provide CSR
4. Verify your domains - must register and verify all top level domains ( cannot hide behind a proxy or redirect - must be accessible for the Apple Servers )
    
    [Host your domain-verification file at the following path for each domain you’re registering](https://developer.apple.com/documentation/applepaywebmerchantregistrationapi/preparing-merchant-domains-for-verification):
    
    `https://[DOMAIN_NAME]/.well-known/apple-developer-merchantid-domain-association`
    
5. Create Merchant Identity Certificate - similar to step 3 but requires generating CSR yourself → for authenticating sessions with Apple Pay servers.
6. Export and test your merchant identity certificate → packaged into a `.p12` file → run openssl commands to split the `.p12` file into `crt.pem` and `key.pem` files

### **Domain Verification 驗證失敗的常見原因:**

https://developer.apple.com/documentation/technotes/tn3173-troubleshooting-issues-with-your-apple-pay-merchant-id-configuration ( Apple doc )

https://developer.apple.com/documentation/technotes/tn3103-apple-pay-on-the-web-troubleshooting-guide# ( Apple doc )

The domain verification file expires after **7 days**, so if you are not able to verify your domain after 7 days you will need to regenerate this file and replace it on your server.

https://support.ecpay.com.tw/16483/

1.檔案位置放置錯誤，導致Apple官方無法連線驗證

2.防火牆沒有打開，導致Apple官方無法連線驗證

3.請確認 SSL 憑證是否有達到A+等級 (https://www.ssllabs.com/ssltest) to check your grade

4.請確認是否因為有開啟UrlScan 進而驗證失敗

5.Apple Pay 僅接受網站為https

## Complete merchant validation ( page 13 )

Once the system launches the payment sheet, the merchant validation process is automatically
triggered and a call to `onmerchantvalidation` is made. In order for merchant validation to be successful, you’ll need to request a merchant session object from the Apple Pay servers.

## Map customer and payment data  ( page 18 )

### Authorize payment with your PSP

Apple Pay passes payment information to your app or website in the form of a PKPayment object (app) or of an ApplePayPayment object (web).
Object contains: transaction ID, payment network, payment token data ( signature, header, encrypted payment data )

### Complete payment

Once you’ve passed the data to PSP and received response, pass the success or failure back into the Apple Pay APIs

Sandbox testing https://developer.apple.com/apple-pay/sandbox-testing/ ( Test Cards for App and Web )

Detailed Diagrams see page 23 for Web version ( Safari )
