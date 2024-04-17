# React Native VoveSDK Documentation

## Introduction

The React Native VoveSDK facilitates easy integration of ID verification and KYC (Know Your Customer) compliance into mobile applications, supporting both iOS and Android platforms. This wrapper abstracts the complexity of interacting with the native VoveSDK, providing a simplified, promise-based JavaScript API for React Native developers.

## Installation

To include the React Native VoveSDK in your project, install it via npm or Yarn:

bashCopy code

```bash
npm i @vove-id/react-native-sdk
```

# or

```bash
yarn add @vove-id/react-native-sdk
```

This package comes bundled with all necessary native dependencies, so there's no need for additional modifications to your `Podfile` or `build.gradle`.

## Usage

The core functionality of the VoveSDK is to perform ID verification through a straightforward function call, which manages the verification process based on a session token and environment setting.

### Starting ID Verification

To initiate the ID verification process, use the `processIDMatching function. This function requires a configuration object which includes the environment, session token, and optional settings such as vocal guidance and locale. It returns a promise that resolves to indicate the verification outcome.

#### Function Signature

```javascript
processIDMatching(config: VoveConfig): Promise<VoveStatus>
```

+ `config`: Configuration object for the verification process, which includes:
  *   `environment`: Specifies the environment for the SDK to operate in. Can be `VoveEnvironment.Production` or `VoveEnvironment.Sandbox`.
  *   `sessionToken`: A token generated by your backend, used to initiate the ID verification session.
  *   `enableVocalGuidance?`: Optional boolean to enable vocal guidance during the verification process.
  *   `locale?`: Optional locale setting for localizing the verification process (see below for details).
#### Example Usage

```javascript
import { processIDMatching, VoveEnvironment, VoveLocale } from '@vove-id/react-native-sdk';

const config = {
  environment: VoveEnvironment.Production,
  sessionToken: 'your_session_token_here',
  enableVocalGuidance: true,
  locale: VoveLocale.EN
};

processIDMatching(config)
  .then((status) => {
    switch (status) {
      case 'success':
        console.log('Verification successful.');
        break;
      case 'pending':
        console.log('Verification pending.');
        break;
      case 'canceled':
        console.log('Verification canceled.');
        break;
      default:
        console.log('Unexpected status:', status);
    }
  })
  .catch((error) => {
    console.error('Verification failed:', error);
  });
```

### Handling Verification Results

The promise returned by `processIDMatching` will:

- Resolve with a status string for "success", "pending", or "canceled" scenarios, indicating the verification outcome.
- Reject in the case of a "failure", providing an error object detailing the failure reason.

### Localization with VoveLocale

The SDK supports multiple languages for ID verification processes. To use this feature, specify the `locale` in the `VoveConfig` when starting the verification:

-   `VoveLocale.EN`: English
-   `VoveLocale.FR`: French
-   `VoveLocale.AR`: Arabic
-   `VoveLocale.AR_MA`: Moroccan Arabic

### Enabling Vocal Guidance

To enhance the user experience during ID verification, vocal guidance can be enabled. Set the `enableVocalGuidance` flag in the `VoveConfig` object to `true`. This feature is especially useful for helping users through the verification process in a clear and guided manner.

## Troubleshooting

Ensure the session token is correctly generated and passed, and that the appropriate environment is selected based on your application's stage (development or production). For unresolved issues, contact support with detailed information about the problem, including error messages and the steps leading up to the issue.

## Support

For further assistance or inquiries about the React Native VoveSDK, please reach out to our support team.
