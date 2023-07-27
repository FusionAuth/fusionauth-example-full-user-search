## Client-side Password Validation Example

FusionAuth provides password rules, configurable at the [tenant level](https://fusionauth.io/docs/v1/tech/core-concepts/tenants). These include checks on a password value such as:

* a password must have one special character
* a password length must be at least 12 characters, in lowercase, uppercase, or a combination including special characters
* a password must contain a numeric character

The [latest guidance from NIST recommends avoiding such rules](https://fusionauth.io/articles/security/breached-password-detection#what-does-nist-have-to-say-about-breached-password-detection) but if you have internal or external policies requiring password complexity rules, FusionAuth supports it.

These password rules are enforced in the hosted HTML login pages, but only after the user has submitted the form. They are also available as freemarker variables on the [registration page](https://fusionauth.io/docs/v1/tech/themes/template-variables#oauth-register) and the [change password page](https://fusionauth.io/docs/v1/tech/themes/template-variables#oauth-change-password-form).

This example shows how to use the `passwordValidationRules` freemarker variables to offer user feedback client-side using JavaScript, in the hosted login pages. It will also disable submission of the form if the rules are not met.

To use this script, make `FusionAuthPasswordChecker.js` available at a public URL or modify the FusionAuth template files to include this JavaScript on the registration page and change password pages. 

```
<script src="https://yourcdn.example.com/path/to/FusionAuthPasswordChecker.js"></script>
```

This JavaScript expects the names and DOM structure of the pages to be the same as the default theme structure. If you've modified your theme, this code will be a starting point, but is not guaranteed to work.

You'll also need to create CSS classes `validation` and `ok` to visually inform your users about the status of their password.

Password rules are also available via an [unauthenticated API call](https://fusionauth.io/docs/v1/tech/apis/tenants#retrieve-the-password-validation-rules) if you'd prefer to build your own validation logic without using JavaScript. This might be useful for a mobile application, for example.

