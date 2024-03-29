React Native VoveSDK Documentation
==========================================

Introduction
------------

The React Native VoveSDK facilitates easy integration of ID verification and KYC (Know Your Customer) compliance into mobile applications, supporting both iOS and Android platforms. This wrapper abstracts the complexity of interacting with the native VoveSDK, providing a simplified, promise-based JavaScript API for React Native developers.

Installation
------------

To include the React Native VoveSDK in your project, install it via npm or Yarn:

bashCopy code

```bash
npm install react-native-vove-sdk
```
# or

```bash
yarn add react-native-vove-sdk
```

This package comes bundled with all necessary native dependencies, so there's no need for additional modifications to your `Podfile` or `build.gradle`.

Usage
-----

The core functionality of the VoveSDK is to perform ID verification through a straightforward function call, which manages the verification process based on a session token and environment setting.

### Starting ID Verification

To initiate the ID verification process, use the `processIDMatching` function. This function requires a session token (obtained from your backend server) and an environment setting. It returns a promise that resolves to indicate the verification outcome.

#### Function Signature

```javascript
processIDMatching(env: VoveEnvironment, sessionToken: string): Promise<string>
```

-   env: Specifies the environment for the SDK to operate in. Can be `VoveEnvironment.Production` or `VoveEnvironment.Development`.
-   sessionToken: A token generated by your backend, used to initiate the ID verification session.

#### Example Usage

```javascript

import { processIDMatching, VoveEnvironment } from 'react-native-vove-sdk';

processIDMatching(VoveEnvironment.Production, "your_session_token_here")
    .then(status => {
    switch (status) {
        case "success":
        console.log("Verification successful.");
        break;
        case "pending":
        console.log("Verification pending.");
        break;
        case "canceled":
        console.log("Verification canceled.");
        break;
        default:
        console.log("Unexpected status:", status);
      }
    })
    .catch(error => {
        console.error("Verification failed:", error);
    });
```

### Handling Verification Results

The promise returned by `processIDMatching` will:

-   Resolve with a status string for "success", "pending", or "canceled" scenarios, indicating the verification outcome.
-   Reject in the case of a "failure", providing an error object detailing the failure reason.

### API Reference

#### processIDMatching

Initiates an ID verification session with the VoveSDK.

-   Parameters:
    -   `env: VoveEnvironment`: The operating environment for the SDK.
    -   `sessionToken: string`: A session token for the verification process.
-   Returns: A promise that resolves with the verification status (`"success"`, `"pending"`, or `"canceled"`) or rejects in case of failure.

#### VoveEnvironment

An enumeration that specifies the SDK's operating environment:

-   `Production`: Use for production builds.
-   `Development`: Use for development or testing.

Troubleshooting
---------------

Ensure the session token is correctly generated and passed, and that the appropriate environment is selected based on your application's stage (development or production). For unresolved issues, contact support with detailed information about the problem, including error messages and the steps leading up to the issue.

Support
-------

For further assistance or inquiries about the React Native VoveSDK, please reach out to our support team.
