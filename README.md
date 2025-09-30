# EmpowerMind Deep Links Configuration

This repository contains the configuration files needed for deep linking in the EmpowerMind mobile application.

## 📁 Files

- `.well-known/apple-app-site-association` - iOS Universal Links configuration
- `.well-known/assetlinks.json` - Android App Links configuration
- `index.html` - Test page with sample deep links

## 🚀 Setup Instructions

### 1. GitHub Pages Setup
1. Fork or clone this repository
2. Go to repository Settings → Pages
3. Set Source to "Deploy from a branch"
4. Select "main" branch
5. Set custom domain to `deeplinks.empowermind.tech`
6. Enable "Enforce HTTPS"

### 2. DNS Configuration
Add this CNAME record to your domain DNS:
```
deeplinks → empowermindprod.github.io
```

### 3. Mobile App Configuration
Update your mobile app with the configurations provided in the other files in this repository.

## 🔗 Test Links

After setup, test these URLs:
- `https://deeplinks.empowermind.tech/app/home`
- `https://deeplinks.empowermind.tech/course/123`
- `https://deeplinks.empowermind.tech/lesson/456`
- `https://deeplinks.empowermind.tech/profile/user`

## 📱 App Details

- **iOS Bundle ID**: `com.empowermind.elvira.fediuchko`
- **Android Package**: `com.empowermind`
- **Apple Team ID**: `PSWA65N6D2`
- **SHA256 Fingerprint**: `EF:91:1B:5C:9D:87:27:EC:C8:56:44:EC:B3:73:B5:93:60:48:CE:A0:C6:CE:2E:2D:C5:33:73:31:D3:A3:10:2F`
