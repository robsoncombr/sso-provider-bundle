# SSO Provider for Directus

#### With the goal of transforming Directus into a centralized authentication hub for your organization's applications.

#### An extension that allows Directus to function as a Single Sign-On (SSO) Provider, using it's own auth system as IdP, allowing external applications to authenticate users through your Directus instance, or even secondary instances of it.

## Overview

This extension expands Directus's authentication capabilities by implementing SSO provider endpoints, allowing applications to delegate their authentication to your Directus instance. It leverages Directus's robust user management system to serve as a central authentication authority.

## Core Features

- SSO Provider Endpoints: 
  - `/oauth/authorize` - Handles initial authentication requests
  - `/oauth/token` - Issues access and refresh tokens
  - `/oauth/userinfo` - Provides authenticated user information
  - `/oauth/.well-known/openid-configuration` - Discovery endpoint for OIDC clients

- Client Application Management:
  - Register and manage trusted applications
  - Configure allowed redirect URIs
  - Set client credentials (ID and secret)
  - Define allowed scopes per client

- User Authentication Flow:
  - Branded login interface using Directus's existing authentication
  - Support for remember-me functionality
  - Session management across applications
  - Single logout capability

## Implementation Benefits

- Unified User Base: Use Directus's existing user management system
- Role-Based Access: Leverage Directus's role system for application access
- Audit Trail: Track authentication events through Directus's activity log
- Token Management: Built-in handling of OAuth tokens and sessions

## Authentication Flows

1. Authorization Code Flow
   - Secure authentication for web applications
   - PKCE support for mobile and native applications

2. Implicit Flow (Optional)
   - Legacy support for older applications
   - Configurable on a per-client basis

## Technical Integration

```typescript
// Example client configuration
{
  client_id: "your-client-id",
  client_secret: "your-client-secret",
  redirect_uris: ["https://your-app.com/callback"],
  allowed_scopes: ["openid", "profile", "email"],
  token_endpoint_auth_method: "client_secret_basic"
}
```

## Security Features

- PKCE Support: Enhanced security for public clients
- Token Encryption: Secure token storage and transmission
- Rate Limiting: Prevent brute force attacks
- Session Management: Configurable session lifetimes
- Scope Control: Fine-grained access control per client

## Getting Started

1. Install the extension:

Refer to the [Official Guide](https://docs.directus.io/extensions/installing-extensions.html) for details on installing the extension from the Marketplace or manually.

2. Configure the extension in your Directus settings:
```javascript
{
  "sso_provider": {
    "issuer": "https://your-directus-instance.com",
    "token_lifetime": 3600,
    "refresh_token_lifetime": 86400
  }
}
```

This extension is ideal for organizations looking to:
- Centralize authentication across multiple applications
- Maintain a single source of truth for user data
- Implement secure and standardized authentication flows
- Reduce development overhead for new applications

## Motivation

First, from my own frustration for trying to adapt to some existing solution, 😥 be it free or paid, but without having found any that really meets some customizations that I need. You can bet that the time and effort that I have already invested in this topic can be considered incalculable at this point.

So, today, working on exactly this subject, I found a not so old discussion about it:
- [Directus as an SSO provider #23786](https://github.com/directus/directus/discussions/23786)

The idea that others are looking for similar solutions motivates us, as it confirms that we are in the right direction, thanks to [@beasteers](https://github.com/beasteers), author of the aforementioned discussion. 🙏

And last but not least, Directus deserves a functionality like this 🚀 -- besides it will be really useful for my projects and many other people. So I decided to challenge myself in this endeavor.

👊 Your collaboration is very welcome in any way, I will be available to work together, receive opinions, suggestions, evaluations and testing, and why not a Pull Request that can save the day.

## License and Maintenance

This project is licensed under the MIT License.

Initial development and maintenance by [@robsoncombr](https://github.com/robsoncombr)

Original Repository: https://github.com/robsoncombr/sso-provider-bundle