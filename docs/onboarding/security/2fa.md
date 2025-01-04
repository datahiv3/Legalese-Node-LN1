# Two-Factor Authentication

[![Website](https://img.shields.io/badge/Register-DataHive_Nodes-blue)](https://www.datahive.network/nodes)
[![Twitter](https://img.shields.io/badge/Twitter-DataHive-blue)](https://x.com/getdatahive)
[![Telegram](https://img.shields.io/badge/Telegram-DataHive-blue)](https://t.me/datahiveofficial)
[![Quest](https://img.shields.io/badge/Quest-DataHive-blue)](https://quest.intract.io/project/datahive-h_lpnt)
[![Email](https://img.shields.io/badge/Email-team@datahive.network-blue)](mailto:team@datahive.network)

The DataHive network requires [node operators](/docs/onboarding/nodes.md) to implement robust two-factor authentication (2FA) to enhance security and protect network operations.

## Supported 2FA Methods

**Authenticator Apps**
- Google Authenticator
- Authy
- Microsoft Authenticator
- YubiKey Authenticator

## Implementation Requirements

**Setup Process**
- Generate unique secret key per operator
- QR code generation for easy app pairing
- Backup code generation and secure storage
- Recovery email verification

## Security Features

**Authentication Flow**
- Time-based one-time passwords (TOTP)
- 30-second code refresh interval
- Rate limiting on failed attempts
- Session management and timeout controls

## Recovery Options

**Account Recovery**
- Backup codes (one-time use)
- Secondary device verification
- Support ticket verification process
- Identity verification requirements

## Best Practices

**Security Recommendations**
- Use dedicated devices for authentication
- Enable app-level security features
- Regular backup code verification
- Periodic security audits

## Integration Points

**System Integration**
- [Node dashboard](/docs/onboarding/dashboard.md) login
- [Wallet operations](/docs/onboarding/wallets.md)
- [Critical operations](/docs/onboarding/operations.md)
- [Administrative functions](/docs/onboarding/admin.md)

*Note: Two-factor authentication is mandatory for all node operators to ensure network security and protect against unauthorized access.*
