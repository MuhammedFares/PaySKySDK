
## PaySky Button SDK

The PaySky Button SDK allows developers to integrate PaySky's payment solution into Android apps quickly and easily.

## Getting Started

These instructions will help you get a copy of the project up and running locally for development and testing.

### Prerequisites

Before using the SDK, ensure you have the following tools installed:

```
1. JDK installed on your machine (minimum version 1.7).
2. Android Studio.
3. Create a new Android project in Android Studio or use an existing project with minSdkVersion of 19.
4. Ensure AndroidX compatibility.
```

### Installing

Follow these steps to integrate the SDK into your Android project.

```
1. Open your Android project.
2. In the project-level `build.gradle` file, under `allprojects {}`, add the following repository:
   maven { url 'https://jitpack.io' }

Example:
allprojects {
    repositories {
        maven { url 'https://jitpack.io' }
    }
}

3. In the app-level `build.gradle` file, under `dependencies {}`, add:
   implementation 'com.github.MuhammedFares:PaySkySDK:v1.0.1'

Example:
dependencies {
    implementation 'com.github.MuhammedFares:PaySkySDK:v1.0.1'
}

4. Sync your project.
```

### Using the SDK

To use the PaySky SDK, you must first obtain your Merchant ID and Terminal ID from PaySky.

1. **Initialize PayButton:**

   Create an instance of `PayButton` and pass the required parameters:

   ```java
   PayButton payButton = new PayButton(context);
   
   payButton.setMerchantId(merchantId); // Merchant ID
   payButton.setTerminalId(terminalId); // Terminal ID
   payButton.setAmount(amount); // Payment amount
   payButton.setCurrencyCode(currencyCode); // Currency code [Optional]
   payButton.setMerchantSecureHash("Merchant secure hash"); // Merchant secure hash
   payButton.setTransactionReferenceNumber("reference number"); // Unique transaction reference number
   payButton.setProductionStatus(PRODUCTION); // Use 'npg' for testing environment
   payButton.setLang(localLang);  // Set language (e.g., "en" or "ar")
   ```

2. **Generate Transaction:**

   To initiate the transaction, call `createTransaction`:

   ```java
   payButton.createTransaction(new PayButton.PaymentTransactionCallback() {
       @Override
       public void onCardTransactionSuccess(SuccessfulCardTransaction cardTransaction) {
           paymentStatusTextView.setText(cardTransaction.toString());
       }

       @Override
       public void onWalletTransactionSuccess(SuccessfulWalletTransaction walletTransaction) {
           paymentStatusTextView.setText(walletTransaction.toString());
       }

       @Override
       public void onError(Throwable error) {
           paymentStatusTextView.setText("Transaction failed: " + error.getMessage());
       }
   });
   ```

   The callback methods include:
   - **onCardTransactionSuccess**: Called when the transaction is successful via card payment.
   - **onWalletTransactionSuccess**: Called when the transaction is successful via wallet payment.
   - **onError**: Called if the transaction fails.

### Resolving Dependency Conflicts

In case of version conflicts with dependencies such as OkHttp, Retrofit, or EventBus, you can force a specific version by adding the following to your `build.gradle` file:

```groovy
configurations.all {
    resolutionStrategy {
        force 'com.google.code.gson:gson:2.8.5'  // Specify the required version
    }
}
```

### Deployment

1. Before deploying your app, ensure you’ve received your Merchant ID and Terminal ID from PaySky.
2. Always secure your Merchant ID and Terminal ID. Encrypt them before storing in your project.

## Built With

- [Retrofit](http://square.github.io/retrofit/) - Networking library for Android.
- [EventBus](https://github.com/greenrobot/EventBus) - Simplifies communication between components.

## Authors
** Muhammed Fares ** - @MuhammedFares 
**PaySky Company** - [PaySky](https://www.paysky.io)

