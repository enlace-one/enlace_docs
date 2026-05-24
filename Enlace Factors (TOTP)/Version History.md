# Enlace Factors Version History

## 1.4
Web Release: 5.24.2026
Extension Release: 5.24.2026

Added Features:
- Manual workaround if Okta registration fails due to CORS

Bug Fixes:
- Autofill always says extension is locked


## 1.3
Web Release: 5.1.2026
Extension Release: 5.1.2026

Added Features:
- Converted temporary browser secret storage back to session from background script. The background script method is not reliable in manifest v3 and other versions are deprecated.
- Added a possible fix to Okta MFA code storage in some contexts

## 1.2
Web Release: 4.19.2026
Extension Release: 4.20.2026

Added Features:
- Change password form
- Remember Devices
- Forget Devices
- Clear Sessions
- SRP Login - Plaintext password only set to AWS on create/change PW, not login

Removed Features:
- Removed Set MFA Preference. It's too easy for users to lock themselves out using this feature.

## 1.1
Web Release: 4.12.2026
Extension Release: 4.13.2026

Added Features:
- Remember Usernames
- TOTP Priority
- Better input validation 
- Improved signup link
- Improved security for temporary browser secret storage (background script)
- New API URL
- Optional PIN in extension, mandatory in web version

## 1.0
Web Release: 4.8.2026
Extension Release: 4.8.2026

The initial release