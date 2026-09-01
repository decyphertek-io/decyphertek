# Privacy Policy

**Last Updated:** September 1, 2026

## Our Commitment to Your Privacy

At CloudTek, we take your privacy seriously. CloudTek manages your cloud infrastructure credentials, and this Privacy Policy explains exactly how that data is handled.

## Data Collection

**We do not collect any personal data or user information.**

CloudTek is designed with privacy as a core principle. This means:

- **No servers, no accounts** - CloudTek has no backend that could receive your data
- **No analytics** - We don't use analytics or tracking tools
- **No crash reporting** - We don't transmit crash reports or diagnostics
- **No advertising** - CloudTek contains no advertising SDKs
- **Nothing sent to us** - The app never transmits any information to the CloudTek developers

## Your Credentials

Your cloud provider credentials and SSH private keys are stored only in an encrypted vault on your device:

- **Encrypted local vault** - Credentials are encrypted with AES-256-GCM, with key material bound to your device's secure hardware keystore (Android Keystore)
- **Never leave your device** - Your credentials are never uploaded, synced, or backed up by CloudTek
- **No intermediary** - No CloudTek server sits between you and your cloud resources

## Cloud Provider Connections

When you initiate an action (such as listing or launching VMs):

- **Direct connections only** - CloudTek connects directly to the cloud provider you configured (AWS, Azure, or GCP)
- **Your credentials, your control** - All requests use your own credentials and happen only when you act
- **We don't see your infrastructure** - We have no access to your cloud resources or activity

## Optional Server Pairing

CloudTek can optionally pair with a self-hosted server for automation features:

- **Your infrastructure** - The server component runs entirely on infrastructure you control
- **No data to us** - Nothing you do with a paired server is visible to Decyphertek

## SSH Terminal

- **Keys stay in the vault** - SSH private keys are stored only in your device's encrypted vault
- **You choose the targets** - The terminal connects only to hosts you explicitly configure

## Permissions

CloudTek requests no dangerous permissions. Internet access is used only to reach the cloud providers and hosts you configure.

## Data Deletion

Use the "Wipe device" option in Settings to permanently destroy the vault, all credentials, SSH keys, profiles, and the audit log. You are always in full control of your data.

## Changes to This Policy

We may update this Privacy Policy from time to time. Any changes will be posted on this page with an updated "Last Updated" date.

## Contact Us

If you have any questions about this Privacy Policy, please contact us at:

- [GitHub Issues](https://github.com/decyphertek-io/CloudTek)
- [Website](https://decyphertek.io/)

## Your Rights

You have complete control over your data because it never leaves your device. You can use CloudTek with confidence knowing that your privacy is protected by design.

---

*This privacy policy reflects our commitment to user privacy and transparency.*
