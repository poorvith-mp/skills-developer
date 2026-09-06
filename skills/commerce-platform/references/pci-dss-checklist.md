# PCI-DSS v4.0 Quick Compliance Checklist

## Requirement 1: Network Security Controls
- [ ] Firewall rules reviewed every 6 months
- [ ] Default credentials changed on all network devices

## Requirement 3: Protect Stored Account Data
- [ ] PAN (Primary Account Number) never stored in plaintext
- [ ] Encryption keys managed with proper key rotation

## Requirement 4: Protect Data in Transit
- [ ] TLS 1.2+ enforced for all cardholder data transmission
- [ ] Certificates valid and properly configured

## Requirement 6: Secure Systems & Software
- [ ] Security patches applied within 30 days of release
- [ ] Custom code reviewed for OWASP Top 10 vulnerabilities

## Requirement 8: Strong Access Controls
- [ ] MFA required for all administrative access to cardholder data environments
- [ ] Unique IDs for all users (no shared accounts)

## Key Rules for Developers
- **NEVER** log full card numbers, CVVs, or magnetic stripe data
- **ALWAYS** use client-side tokenization (Stripe Elements, Braintree Hosted Fields)
- **NEVER** store CVV/CVC codes after authorization
