# YUG Captcha Service Documentation

## Overview

YUG Captcha Service provides a secure and reliable CAPTCHA solution to protect your applications from automated attacks.

## Key Concepts

### Identity Key

The `identity_key` is a core component of YUG Captcha Service. It is a user-assigned identity token with the following characteristics:

- **Unique Identification**: Uniquely identifies the requester across all API calls
- **Consistency**: The same `identity_key` must be used in all related requests, ensuring CAPTCHA challenges and verification are linked to the same user session
- **Security**: Through consistent identity tokens, the service can securely track and validate CAPTCHA challenges

## API Usage

### Request Format

All requests should include the following basic structure:

```json
{
  "identity_key": "xiaoming",
  "captcha_type": "DIGIT"
}
```

### Usage Scenario

When implementing CAPTCHA in a front-end application, such as during a device login process, it is crucial to ensure that the `identity_key` is unique and consistent. A practical approach is to use the device ID as the `identity_key`. This ensures that each device has a unique identifier, maintaining the uniqueness and consistency required for CAPTCHA challenges.

**Example:**

For a mobile app, when a user attempts to log in, the app can generate a request like this:

```json
{
  "identity_key": "device12345", // Use the device ID here
  "captcha_type": "IMAGE"
}
```

By using the device ID as the `identity_key`, you ensure that each CAPTCHA challenge is uniquely tied to the specific device, enhancing security and user experience.

## Business Scenario

The `business_scenario` field in the `FetchImageCaptchaRequest` message is used to specify the context in which the CAPTCHA is being requested. This field serves several important purposes:

1. **Customization of CAPTCHA**: Different business scenarios may require different types or levels of CAPTCHA complexity. For example, a login scenario might use a simpler CAPTCHA, while a financial transaction scenario might require a more complex CAPTCHA to enhance security.

2. **Data Collection and Analysis**: By recording the business scenario, the server can collect and analyze CAPTCHA request data across different contexts. This helps identify which scenarios are more prone to attacks, allowing for targeted security enhancements.

3. **Strategy Adjustment**: The server can dynamically adjust CAPTCHA generation strategies based on the business scenario. For instance, in high-risk scenarios, the server might increase the complexity or frequency of CAPTCHA challenges.

4. **User Experience Optimization**: In certain scenarios, it may be beneficial to reduce the frequency of CAPTCHA challenges to improve user experience. By understanding the business scenario, the server can make smarter decisions about when to present a CAPTCHA.

Overall, the `business_scenario` field provides greater flexibility and intelligence to the CAPTCHA service, enabling it to better meet diverse business needs and security strategies.

### API Reference

- [FetchImageCaptcha](./captcha.proto#fetchimagecaptcharequest)
- [ValidateImageCaptcha](./captcha.proto#validateimagecaptcharequest)
- [FetchSlideCaptcha](./captcha.proto#fetchslidecaptcharequest)
- [ValidateSlideCaptcha](./captcha.proto#validateslidecaptcharequest)
- [ValidateAndRemoveCaptcha](./captcha.proto#validateandremovecaptcharequest)
- [ValidateCaptchaAndIssueToken](./captcha.proto#validatecaptchaandissuetokenrequest)
