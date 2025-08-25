# FxA CMS Localization Repository

This repository contains localization files for Mozilla Accounts (FxA) CMS content. It automatically generates FTL (Fluent Translation List) files from Strapi CMS changes and delivers localized content to users through Pontoon integration.

## Purpose

- Stores FTL files generated from Strapi CMS content
- Bridges content management and localization workflows
- Supports automated localization through webhooks
- Delivers cached localized content at runtime

## Architecture

- **Strapi CMS**: Content management for relying party configurations
- **GitHub**: FTL file storage and version control
- **Pontoon**: Mozilla's localization platform
- **fxa-auth-server**: Webhook processing and API delivery
- **Runtime**: Multi-level caching with fallback strategies

## Workflow

1. **Content Creation** → Strapi CMS updates
2. **Webhook Trigger** → Automated FTL generation
3. **GitHub PR** → Human review and approval
4. **Pontoon Integration** → Community translation
5. **Runtime Delivery** → Cached localization with fallbacks

## Structure

```
locales/
├── en/cms.ftl          # Base English (source of truth)
├── es/cms.ftl          # Spanish translations
├── fr/cms.ftl          # French translations
└── [other-locales]/    # Additional languages
```

## Quick Start

### For Translators
- Access [Pontoon](https://pontoon.mozilla.org/)
- Find FxA project and select language
- Translate strings in CMS localization files

### For Developers
- Monitor automated PRs from Strapi webhooks
- Review generated FTL files before merging
- Test localization with commands below

## Configuration

```bash
FXA_L10N_REPO=mozilla/fxa-cms-l10n
FXA_L10N_BRANCH=main
```

```typescript
ftlUrl: "https://raw.githubusercontent.com/mozilla/fxa-cms-l10n/{branch}/locales/{locale}/cms.ftl"
```

## Testing

```bash
# Test localization
curl "http://localhost:9000/v1/cms/config?clientId={id}&entrypoint={point}" \
  -H "Accept-Language: es-MX"

# Run tests
NODE_ENV=test yarn test test/local/routes/utils/cms/localization.js
```

## Common Issues

- **Empty Config**: Check FTL file availability and cache status
- **Webhook Failures**: Verify secret and Strapi connectivity
- **PR Errors**: Confirm GitHub token permissions
- **Cache Issues**: Clear caches and verify TTL settings

## Resources

- [Complete Workflow Documentation](./accountslocalization.md)
- [FTL Documentation](https://projectfluent.org/fluent/guide/)
- [Pontoon Guide](https://mozilla-l10n.github.io/documentation/)
- [FxA Repository](https://github.com/mozilla/fxa)

## Support

- **Localization**: Mozilla l10n team
- **Technical**: [FxA repository issues](https://github.com/mozilla/fxa)
- **Content**: FxA product team
