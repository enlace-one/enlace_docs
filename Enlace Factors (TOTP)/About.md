# Enlace Factors

Enlace Factors allows for easy access to Multi-Factor Authentication (MFA) Time-based One-Time Password Tokens across your devices while storing them securely - Encrypted using your password just like a password manager would. 

Easily register by scanning the QR code in the the current tab (using the browser extension), in a file, or with your camera.

Enlace Factors has support for the standard Time-based One-Time Password (TOTP) format as well as for Okta Verify's QR code format.

## Why not Use My Password Manager?

If your password manager has both your passwords and your MFA, then that is one single point of failure. If it is compromised, and there have been plenty of vulnerabilities in password managers that could compromise it, then the attacker has instant access to your accounts.

If you use your password manager for just your passwords and Enlace Factors for your TOTP, then both would need to be compromised in order to get your account access. 

Just be sure that your Enlace Factors password/TOTP are not both stored in your password manager and vice versa. 

## Get the App

[Install the Browser Extension](https://chromewebstore.google.com/detail/enlace-factors/gkagbinmanpfoeojghjdgkaobmjogcfp)

[Visit the Website](https://factors.enlace.one/)

## More About the Extension

The extension is one of the best features of Enlace Factors due to the easy set up and use of codes.

You can configure a keyboard shortcut so you can automatically enter the code matching the active tab to get you into your account as quickly as possible. 

## Security

Your TOTPs are encrypted with your master key and a unique salt for each one before being sent to be stored in AWS. 

Your master key is based on your password, salted with your email and a public pepper. 

The encryption technologies used are: AES-GCM, SHA-265, and PBKDF2

Your TOTPs are never stored client side in the web version or extension.

You have the option on the browser extension to also encrypt the stored tokens with a unqiue PIN. That is required on the web version as session storage is used.