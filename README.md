<p align="center">
    <img title="Flutterwave" height="200" src="https://flutterwave.com/images/logo-colored.svg" width="50%"/>
</p>

# Flutterwave Android SDK

Flutterwave's Android SDK can be used to integrate the Flutterwave payment gateway into your android app. You can drop our payment sdk inside your app easily and it performs all its processing without leaving your app also choose any payment option to show directly

The payment methods currently supported are Cards, USSD, Mpesa, GH Mobile Money, UG Mobile Money, ZM Mobile Money, Rwanda Mobile Money, Franc Mobile Money, US ACH, UK Bank, SA Bank, Nigeria Bank Account, Nigeria Bank Transfer, Barter Mobile Wallet.
 

<img alt="Screenshot of Drop-In" src="https://i.imgur.com/UZZkC6e.png" width="900"/>

## Before you begin
- Ensure you have your test (and live) [API keys](https://developer.flutterwave.com/docs/api-keys).

## Requirements
- The minimum supported SDK version is 15
- Rave android sdk 1.0.50 and above only supports projects that have been migrated to [androidx](https://developer.android.com/jetpack/androidx/). For more information, read Google's [migration guide](https://developer.android.com/jetpack/androidx/migrate).

## Adding it to your project

For quick sample implementation, check here https://github.com/mikelis135/RaveEmbed


**Step 1.** Add it in your root build.gradle at the end of repositories:
```groovy
    allprojects {
		repositories {
			//...
			maven { url 'https://jitpack.io' }
		}
	}
```
**Step 2.** Add the dependency

If you want to use the default Drop In UI, add the `rave-android` module dependency and fragment dependency. 
Check https://developer.android.com/training/basics/fragments/pass-data-between for more information and the latest version of the fragment library
```groovy
    dependencies {
	     implementation 'implementation 'com.github.mikelis135:rave-android:1.1.13'
	     implementation 'androidx.fragment:fragment:1.3.0-alpha04'
	}
```
**Step 3.** Add the  `INTERNET` permission to your android manifest

     <uses-permission android:name="android.permission.INTERNET" /> 


> The steps below show how to use the Flutterwave Android SDK as a Drop-in UI (all the views for the payment process are handled by the SDK).

## Usage
### For using the default UI
###  1. Create a `RaveUiManager` instance
Set the public key, encryption key and other required parameters. The `RaveUiManager` accepts a mandatory instance of the calling `Fragment` and an instance of the parent `Activity`.

        new RaveUiManager(fragment).setAmount(amount)
                        .setCurrency(currency)
                        .setEmail(email)
                        .setfName(fName)
                        .setlName(lName)
                        .setNarration(narration)
                        .setPublicKey(publicKey)
                        .setEncryptionKey(encryptionKey)
                        .setTxRef(txRef)
                        .setPhoneNumber(phoneNumber, boolean)
                        .acceptAccountPayments(boolean)
                        .acceptCardPayments(boolean)
                        .acceptMpesaPayments(boolean)
                        .acceptAchPayments(boolean)
                        .acceptGHMobileMoneyPayments(boolean)
                        .acceptUgMobileMoneyPayments(boolean)
                        .acceptZmMobileMoneyPayments(boolean)
                        .acceptRwfMobileMoneyPayments(boolean)
                        .acceptSaBankPayments(boolean)
                        .acceptUkPayments(boolean)
                        .acceptBankTransferPayments(boolean)
                        .acceptUssdPayments(boolean)
                        .acceptBarterPayments(boolean)
                        .acceptFrancMobileMoneyPayments(boolean)
                        .allowSaveCardFeature(boolean)
                        .onStagingEnv(boolean)
                        .setMeta(List<Meta>)
                        .withTheme(styleId)
                        .isPreAuth(boolean)
                        .setSubAccounts(List<SubAccount>)
                        .shouldDisplayFee(boolean)
                        .showStagingLabel(boolean)
			    .embedFragment(int, appcompatActivity)
                        .initialize();


<details>
    <summary>Function Definitions</summary>


| Function        | Parameter           | Type | Required  |
| ------------- |:-------------:| -----:| -----:|
| setAmount(amount)      |  This is the amount to be charged from card/account | `double` | Required
| setCurrency(currency) | This is the specified currency to charge the card in | `String` | Required
| setfName(fName) | This is the first name of the card holder or the customer  | `String` | Required
| setlName(lName) | This is the last name of the card holder or the customer | `String` | Required
| setEmail(email) | This is the email address of the customer | `String` | Required
| setNarration(narration) | This is a custom description added by the merchant. For `Bank Transfer` payments, this becomes the account name of the account to be paid into. See more details [here](https://developer.flutterwave.com/v2.0/reference#pay-with-bank-transfer-nigeria). | `String` | Not Required
| setPublicKey(publicKey) | Merchant's public key. Get your merchant keys here for [ staging](https://flutterwavedevelopers.readme.io/blog/how-to-get-your-staging-keys-from-the-rave-sandbox-environment) and [live](https://flutterwavedevelopers.readme.io/blog/how-to-get-your-live-keys-from-the-rave-dashboard)| `String` | Required
| setEncryptionKey(encryptionKey) | Merchant's encryption key. Get your merchant keys here for [ staging](https://flutterwavedevelopers.readme.io/blog/how-to-get-your-staging-keys-from-the-rave-sandbox-environment) and [live](https://flutterwavedevelopers.readme.io/blog/how-to-get-your-live-keys-from-the-rave-dashboard) | `String` | Required
| setTxRef(txRef) | This is the unique reference, unique to the particular transaction being carried out. It is generated by the merchant for every transaction | `String` | Required
| setPhoneNumber(phoneNumber) | This sets the customer's phone number. This functions is also overloaded to allow you specify whether the customer can edit their phone number as such: `setPhoneNumber(phoneNumber,false)`. When set to false, the user will not be able to change the number you set here.| `String`<br/><br/>Optional overloads:<br/>`String`, `boolean` | Not Required
| acceptAccountPayments(boolean) | Set to `true` if you want to accept payments via bank accounts, else set to `false`. | `boolean` | Not Required
| acceptCardPayments(boolean) | Set to `true` if you want to accept payments via cards, else set to `false` | `boolean` | Not Required |
| acceptMpesaPayments(boolean) | Set to `true` if you want to accept Mpesa payments, else set to `false` . For this option to work, you should set your country to `KE` and your currency to `KES` | `boolean` | Not Required |
| acceptGHMobileMoneyPayments(boolean) | Set to `true` if you want to accept Ghana mobile money payments, else set to `false` . For this option to work, you should set your country to `GH` and your currency to `GHS`| `boolean` | Not Required |
| acceptUgMobileMoneyPayments(boolean) | Set to `true` if you want to accept Uganda mobile money payments, else set to `false` . For this option to work, you should set your country to `UG` and your currency to `UGX`| `boolean` | Not Required |
| acceptZmMobileMoneyPayments(boolean) | Set to `true` if you want to accept Zambia mobile money payments, else set to `false` . For this option to work, you should set your country to `NG` and your currency to `ZMW`. `MTN` is the only available network at the moment, see more details in the [API documentation](https://developer.flutterwave.com/reference#zambia-mobile-money).| `boolean` | Not Required |
| acceptRwfMobileMoneyPayments(boolean) | Set to `true` if you want to accept Rwanda mobile money payments, else set to `false` . For this option to work, you should set your country to `NG` and your currency to `RWF`. See more details in the [API documentation](https://developer.flutterwave.com/reference#rwanda-mobile-money).| `boolean` | Not Required |
| acceptSaBankPayments(boolean) | Set to `true` if you want to accept South African direct bank account payments, else set to `false` . For this option to work, you should set your country to `ZA` and your currency to `ZAR`.| `boolean` | Not Required |
| acceptUkPayments(boolean) | Set to `true` if you want to accept UK Bank Account payments, else set to `false` . For this option to work, you should set your country to `NG`, set currency to `GBP`, set accountbank `String`, set accountname `String`, set accountnumber `String`, set is_uk_bank_charge2 `true`, set payment_type `account`. `Please use your live credentials for this` | `boolean` | Not Required |
| acceptAchPayments(boolean) | Set to `true` if you want to accept US ACH charges from your customers, else set to `false` . For this option to work, you should set your country to `US` and your currency to `USD`. You also have to set `acceptAccountPayments(true)`| `boolean` | Not Required |
| acceptBankTransferPayments(boolean) | Set to `true` if you want to accept payments via bank transfer from your customers, else set to `false`. This option is currently only available for Nigerian Naira. <br/><br/><strong>Note:</strong> By default, the account numbers generated are dynamic. This method has been overloaded for more options as shown below:<br><ul><li>To generate static (permanent) accounts instead, pass in `true` as a second parameter. E.g. <br/>```acceptBankTransferPayments(true, true)```</li><li>To generate accounts that expire at a certain date, or after a certain number of payments, pass in integer values for `duration` and `frequency` as such: <br/>```acceptBankTransferPayments(true, duration, frequency)``` </li></ul>You can get more details in the [API documentation](https://developer.flutterwave.com/v2.0/reference#pay-with-bank-transfer-nigeria).| `boolean`<br/><br/>Optional overloads:<br/>`boolean`, `boolean`<br/><br/>`boolean`, `int`, `int` | Not Required |
| acceptUssdPayments(boolean) | Set to `true` if you want to accept payments via USSD transfer from your customers, else set to `false` . This option is currently only available for the Nigerian Naira.| `boolean` | Not Required |
| acceptBarterPayments(boolean) | Set to `true` if you want to accept payments via Barter from your customers, else set to `false`.| `boolean` | Not Required |
| acceptFrancMobileMoneyPayments(boolean) | Set to `true` if you want to accept Francophone mobile money payments, else set to `false` . For this option to work, you should set your country to `NG` and your currency to `XOF` for West African CFA franc like `Ivory Coast` OR `XAF` for Central African CFA franc like `Cameroon` . See more details in the [API documentation](https://developer.flutterwave.com/reference#mobile-money-francophone).| `boolean` | Not Required |
| allowSaveCardFeature(boolean) | Set to `true` if you want to give the user the option to save their cards for future transactions. This option helps them avoid retyping their card details for every transaction. Defaults to `true`.| `boolean` | Not Required |
| onStagingEnv(boolean) | Set to `true` if you want your transactions to run in the staging environment otherwise set to `false`. Defaults to false  | `boolean` | Not Required
| setMeta(`List<Meta>`) | Pass in any other custom data you wish to pass. It takes in a `List` of `Meta` objects | List<Meta> | Not Required
| setSubAccounts(`List<SubAccount>`) | Pass in a `List` of `SubAccount`,if you want to split transaction fee with other people. Subaccounts are your vendors' accounts that you want to settle per transaction. To initialize a `SubAccount` class, do `SubAccount(String subAccountId,String transactionSplitRatio)` or `SubAccount(String subAccountId,String transactionSplitRatio,String transactionChargeType, String transactionCharge)` to also charge the subaccount a fee. [Learn more about split payments and subaccounts](https://developer.flutterwave.com/docs/split-payment).| `List<SubAccount>`| Not Required
| setIsPreAuth(boolean) | Set to `true` to preauthorise the transaction amount. [Learn more about preauthourization](https://developer.flutterwave.com/v2.0/reference#introduction-1). | `int` | Not Required
| withTheme(styleId) | Sets the theme of the UI. | `int` | Not Required
| setPaymentPlan(payment_plan) | If you want to do recurrent payment, this is the payment plan ID to use for the recurring payment, you can see how to create payment plans [here](https://flutterwavedevelopers.readme.io/v2.0/reference#create-payment-plan) and [here](https://flutterwavedevelopers.readme.io/docs/recurring-billing). This is only available for card payments | `String` | Not Required
| shouldDisplayFee(boolean) | Set to `false` to not display a dialog for confirming total amount(including charge fee) that Rave will charge. By default this is set to `true` | `boolean` | Not Required
| showStagingLabel(boolean) | Set to `false` to not display a staging label when in staging environment. By default this is set to `true` | `boolean` | Not Required
| embedFragment(int, appcompatActivity) | Accepts an id of a view (int) and an appcompatActivity and embeds the rave payment ui into the view,   |  int, appcompatActivity | Required
| initialize() | Launch the Rave Payment UI for when using the UI module,   |  N/A | Required

> <strong>Note:</strong> The order in which you call the methods for accepting different payment types is the order in which they will show in the UI.

>  To see a more practical way of using the sdk, head to our sample app in the repository [here](https://github.com/Flutterwave/rave-android/tree/master/app)
</details>


###  2. Handle the response
In the calling Frgament, use the setFragmentResultListener method to receive the payment response as shown below
```java
	getParentFragmentManager().setFragmentResultListener(RAVE_REQUEST_KEY, this, new FragmentResultListener() {
	  
            @Override
            public void onFragmentResult(@NonNull String requestKey, @NonNull Bundle result) {
		
		int resultCode = result.getInt("resultCode");
                int requestCode = result.getInt("requestCode");
		
			/*
			 *  We advise you to do a further verification of transaction's details on your server to be
			 *  sure everything checks out before providing service or goods.
			*/
	
         	if (requestCode == RaveConstants.RAVE_REQUEST_CODE && result != null) {

			String message = result.getString("response");

			    if (message != null) {
				Log.d("rave response", message);
			    }

			    if (resultCode == RavePayActivity.RESULT_SUCCESS) {
				Toast.makeText(requireContext(), "SUCCESS " + message, Toast.LENGTH_SHORT).show();
			    } else if (resultCode == RavePayActivity.RESULT_ERROR) {
				Toast.makeText(requireContext(), "ERROR " + message, Toast.LENGTH_SHORT).show();
			    } else if (resultCode == RavePayActivity.RESULT_CANCELLED) {
				Toast.makeText(requireContext(), "CANCELLED " + message, Toast.LENGTH_SHORT).show();
			    }
		    
          	 }
    }
    
```
Rave's Android SDK
MIT License

Copyright (c) 2020

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
