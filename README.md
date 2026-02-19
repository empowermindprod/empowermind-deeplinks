# Virea Deep Links (Production)

This repository hosts production deep-link infrastructure for the Virea mobile app on `deeplinks.empowermind.tech`.

## Current Status

- Android App Links are configured for production package `com.empowermind.app` only.
- `assetlinks.json` includes both:
  - Google Play App Signing SHA-256 (for Play-installed app)
  - Upload/local signing SHA-256 (for internal/local signed builds)
- iOS Universal Links are configured via `apple-app-site-association`.
- Deep-link landing pages (`index.html` and `404.html`) use Virea branding and elvira-prod color palette.
- Store fallback is enabled:
  - `404.html`: redirect to store only after the second manual tap on `Open App` if app still does not open.
  - `index.html`: deep-link button flow falls back to store when app open fails.

## Repository Files

- `.well-known/apple-app-site-association` - iOS Universal Links statements
- `.well-known/assetlinks.json` - Android Digital Asset Links statements
- `.nojekyll` - required so GitHub Pages serves `.well-known/*` correctly
- `index.html` - public deep-link entry page (Profile/News/Course actions)
- `404.html` - fallback page for unresolved deep-link paths
- `privacy.html` - privacy policy page
- `terms.html` - terms page
- `CNAME` - custom domain binding (`deeplinks.empowermind.tech`)

## Production App Identity

- Domain: `deeplinks.empowermind.tech`
- Android package: `com.empowermind.app`
- iOS app IDs in AASA:
  - `PSWA65N6D2.com.empowermind.elvira.fediuchko`
  - `PSWA65N6D2.com.empowermind.app`
- Android SHA-256 fingerprints in `assetlinks.json`:
  - `E7:D6:89:26:45:72:10:6F:3E:8E:E1:20:31:30:8E:05:86:4E:EF:B1:51:77:47:FF:AF:A0:52:9F:89:76:C8:B4`
  - `EF:91:1B:5C:9D:87:27:EC:C8:56:44:EC:B3:73:B5:93:60:48:CE:A0:C6:CE:2E:2D:C5:33:73:31:D3:A3:10:2F`

## Store Fallback URLs

- Google Play: `https://play.google.com/store/apps/details?id=com.empowermind.app`
- App Store (UA locale): `https://apps.apple.com/ua/app/virea/id6753343760?l=uk`

## Dependencies and External Services

This project is static hosting only; there are no runtime package dependencies (no Node.js, no Flutter, no backend code in this repo).

External dependencies:
- GitHub Pages - static hosting and deployment from `main`
- DNS CNAME - `deeplinks.empowermind.tech -> empowermindprod.github.io`
- Apple Universal Links validation (AASA retrieval)
- Android Digital Asset Links validation (`assetlinks.json`)
- Google Play and App Store listing URLs for fallback routing

Operational notes:
- CDN/browser caching may delay propagation after deploy.
- Android domain verification results may lag after `assetlinks.json` updates.

## Quick Verification

- Hosted files:
  - `https://deeplinks.empowermind.tech/.well-known/assetlinks.json`
  - `https://deeplinks.empowermind.tech/.well-known/apple-app-site-association`
- Android DAL check endpoint example:
  - `https://digitalassetlinks.googleapis.com/v1/assetlinks:check?...`
- Manual device test:
  - open `https://deeplinks.empowermind.tech/profile`
  - verify app opens directly when installed
  - verify store fallback behavior when app is not available/openable
