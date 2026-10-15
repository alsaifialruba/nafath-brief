Version: NAFATH-V1. Your track: Software
Overview
A national single sign-on service lets citizens reach many government services with one account, so every layer must be trustworthy. Software standards define how login works: OpenID Connect proves who the user is, while OAuth 2.0 governs delegated access. Cybersecurity decides how strongly the user is proven, ideally with phishing-resistant methods. The Android app must respect permission limits, and DNS over HTTPS protects name lookups on the network. An AI model that flags suspicious logins adds another layer, but a risk framework must govern it. Finally, Oman's data protection rules shape what the authority may collect, store, and report after a breach. In my track, OpenID Connect, not plain OAuth 2.0, is the standard layer that lets citizens log in once and be identified across services.
Software
OpenID Connect (OIDC) and OAuth 2.0 solve different problems. OAuth 2.0 is an authorization framework: it lets a third-party application obtain limited access to an HTTP service. OIDC is a simple identity layer built on top of OAuth 2.0, adding authentication through an ID Token and standard claims about the user. So OIDC is the one designed for user login, while OAuth 2.0 alone is for delegated access to resources.
Resource: OpenID Connect Core 1.0 - https://openid.net/specs/openid-connect-core-1_0.html
AI
The authority should use the NIST AI Risk Management Framework 1.0 and manage its seven trustworthiness characteristics before launch. For a login-risk model, validity is the foundation: false positives lock out citizens and false negatives miss attackers. It must also be secure against adversarial examples and data poisoning, privacy-enhanced, checked for harmful bias, explainable, and accountable, with human intervention when the model errs. NIST says these characteristics involve trade-offs, so decisions must be justified transparently.
Resource: AI Risks and Trustworthiness (NIST AI RMF 1.0, Section 3) - https://airc.nist.gov/airmf-resources/airmf/3-sec-characteristics/
Mobile
Every Android app runs in a limited-access sandbox, so the login app cannot reach outside data without permission. If it declares dangerous permissions on Android 6.0 or higher, it must request them at runtime. It should ask only in context, when the user starts the feature needing it, explain why when the system suggests a rationale, and keep working if the user denies. Camera, microphone or location requests also offer an "Only this time" option from Android 11.
Resource: Request runtime permissions - Android Developers - https://developer.android.com/training/permissions/requesting
Networking
DNS over HTTPS (DoH) sends each DNS query and response inside an HTTPS exchange. It encrypts DNS traffic and authenticates the server, which protects users from passive surveillance and from attacks that divert queries to rogue servers. It does not hide the user's IP address from the resolver, and HTTPS features like cookies can still help servers correlate requests. It also does not provide DNSSEC's response integrity of DNS answers.
Resource: RFC 8484 - DNS Queries over HTTPS (DoH) - https://datatracker.ietf.org/doc/html/rfc8484
Cybersecurity
An authentication method is phishing-resistant when its protocol prevents secrets and valid outputs reaching a fake verifier, without relying on user vigilance. NIST SP 800-63B-4 recognizes two methods: channel binding and verifier name binding. FIDO2/WebAuthn authenticators and PIV/CAC smart cards qualify. Passwords, one-time passcodes and out-of-band methods such as SMS codes do not, because manually entered outputs can be relayed by an impostor.
Resource: NIST Special Publication 800-63B - https://pages.nist.gov/800-63-4/sp800-63b.html
Data
Oman's Personal Data Protection Law requires explicit consent before processing, after telling people who processes their data and why. Controllers must appoint a data protection officer, keep a processing record, give people a way to exercise their rights, and notify the Ministry of breaches within 72 hours, and affected people when risk is high. Biometric data needs a Ministry permit. State administrative units are exempt from the law, but MTCIT says Circular 6/2024 governs them.
Resource: Governance - Personal Data Protection | MTCIT - https://mtcit.gov.om/sectors/governance/personal
Misconception in My Track
A common belief is that OAuth 2.0 is a login protocol, so an access token proves who the user is. This is wrong. OAuth 2.0 only delegates access to resources; a token says what a client may do, not who signed in. Login needs OpenID Connect, which adds an ID Token and standard user claims on top of OAuth 2.0. Using bare OAuth for login would leave the authority without a standard way to verify identity. The proof is in Section 1, Introduction, of the OpenID Connect Core 1.0 specification.
Open Question
I would verify what Circular 6/2024 requires of government units for consent and breach reporting, since the law itself exempts them, and how that applies to this login service.

