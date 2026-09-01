# Privacy Policy

**Last Updated:** September 1, 2026

## Our Commitment to Your Privacy

At StackTek, we take your privacy seriously. StackTek is self-hosted software that runs entirely on infrastructure you control, and this Privacy Policy explains how data is handled.

## Data Collection

**Decyphertek does not collect any personal data or user information.**

StackTek is designed with privacy as a core principle. This means:

- **No telemetry** - The software contains no analytics, tracking, or phone-home functionality
- **No accounts with us** - StackTek is not operated by Decyphertek; there is no StackTek cloud service and no user registrations with us
- **No visibility into your deployment** - We have no access to your server, your workspaces, or your users

## Self-Hosted Means Your Data Stays With You

StackTek runs on a server you control, so all data it handles stays on that server:

- **Session credentials and authentication data** - Stored on your server only
- **Workspace data** - Anything created in web desktops, AI agents, and apps (files, conversations, configurations) is stored in your server's isolated containers and session directories
- **Logs** - Web server and WAF access logs remain on your server

You, as the operator, are the data controller for your StackTek deployment. Privacy between you and your users is governed by your own policies.

## Security of Data in Transit

StackTek protects data moving between users and the server:

- **TLS everywhere** - All browser sessions are encrypted in transit
- **Per-user isolation** - Every user gets their own isolated container instance
- **Hardened edge** - A web application firewall (OWASP Core Rule Set) guards access
- **No VPN required** - Nothing is exposed beyond the TLS-protected web interface

## If You Use a StackTek Instance Operated by Someone Else

If you access StackTek hosted by another party:

- **That operator controls the server** - Your session data and anything you do inside workspaces can be accessed by the hosting operator
- **Their policy governs** - Direct privacy questions and deletion requests to your operator, not Decyphertek

## Third-Party Services

AI agent workspaces can connect to third-party AI providers configured by the operator:

- **You configure the providers** - AI features only reach the providers whose API keys the operator configures
- **Provider policies apply** - Content sent to those providers is governed by their privacy policies
- **We don't see any of it** - Decyphertek has no access to these interactions

## Data Deletion

- **As the operator** - You can permanently remove all session data and workspace volumes, and delete the session data directories at any time
- **As a user of someone else's instance** - Contact the operator to request deletion of your data

## Changes to This Policy

We may update this Privacy Policy from time to time. Any changes will be posted on this page with an updated "Last Updated" date.

## Contact Us

If you have any questions about this Privacy Policy, please contact us at:

- [GitHub Issues](https://github.com/decyphertek-io/stacktek)
- [Website](https://decyphertek.io/)

## Your Rights

If you operate StackTek, you have complete control over all data because it lives on your infrastructure. Your privacy is protected by design.

---

*This privacy policy reflects our commitment to user privacy and transparency.*
