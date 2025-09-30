# 🚀 Інструкції з налаштування Deep Links для EmpowerMind

## ✅ Що вже зроблено

### 📱 Мобільний додаток
- ✅ Оновлено `android/app/src/main/AndroidManifest.xml` з intent-filter для `empowermind.tech`
- ✅ Створено `ios/Runner/Runner.entitlements` з Associated Domains
- ✅ Оновлено `ios/Runner/Info.plist` з URL schemes для Universal Links
- ✅ Залежність `app_links: ^6.3.3` вже присутня в `pubspec.yaml`
- ✅ Оновлено `lib/bl/deep_links.dart` для обробки empowermind.tech посилань

### 🌐 GitHub Pages файли
- ✅ Створено `.well-known/apple-app-site-association` для iOS
- ✅ Створено `.well-known/assetlinks.json` для Android
- ✅ SHA256 fingerprint отримано: `EF:91:1B:5C:9D:87:27:EC:C8:56:44:EC:B3:73:B5:93:60:48:CE:A0:C6:CE:2E:2D:C5:33:73:31:D3:A3:10:2F`

## 🎯 Наступні кроки

### 1. Створення GitHub репозиторію
```bash
# 1. Створіть новий публічний репозиторій на GitHub
# Назва: empowermind-deeplinks (або будь-яка інша)

# 2. Клонуйте репозиторій локально
git clone https://github.com/ВАШЕ_ІМ_Я/empowermind-deeplinks.git
cd empowermind-deeplinks

# 3. Скопіюйте файли з /Users/vfediuchko/empowermind-deeplinks/
cp -r /Users/vfediuchko/empowermind-deeplinks/* .

# 4. Додайте файли до git
git add .
git commit -m "Add deep links configuration files"
git push origin main
```

### 2. Налаштування GitHub Pages
1. Перейдіть до Settings → Pages у вашому репозиторії
2. **Source**: Deploy from a branch
3. **Branch**: main
4. **Custom domain**: `empowermind.tech`
5. ✅ **Enforce HTTPS** (обов'язково!)

### 3. Налаштування DNS
У вашого реєстратора домену `empowermind.tech` додайте:

**A Records:**
```
@ → 185.199.108.153
@ → 185.199.109.153
@ → 185.199.110.153
@ → 185.199.111.153
```

**CNAME Record:**
```
www → ВАШЕ_ІМ_Я.github.io
```

### 4. Очікування поширення
- DNS зміни можуть зайняти до 24 годин
- GitHub Pages може зайняти до 10 хвилин для активації

## 🧪 Тестування

### Перевірка конфігурації
1. Відкрийте `https://empowermind.tech/.well-known/apple-app-site-association`
2. Відкрийте `https://empowermind.tech/.well-known/assetlinks.json`
3. Обидва файли повинні відкриватися без помилок

### Тестування Deep Links

**Android:**
```bash
# Через ADB
adb shell am start -W -a android.intent.action.VIEW -d "https://empowermind.tech/course/123" com.empowermind

# Або відкрийте посилання в Chrome на пристрої
```

**iOS:**
```bash
# Через симулятор
xcrun simctl openurl booted "https://empowermind.tech/course/123"

# Або відкрийте посилання в Safari на пристрої
```

### Тестові посилання
- `https://empowermind.tech/app/home`
- `https://empowermind.tech/course/123`
- `https://empowermind.tech/lesson/456`
- `https://empowermind.tech/profile/user`
- `https://empowermind.tech/auth/login`

## 🔧 Налаштування мобільного додатка

### Збірка та тестування
```bash
# Android
flutter build apk --release
flutter install

# iOS (потрібен Mac)
flutter build ios --release
# Встановіть через Xcode
```

### Додаткова навігація
У файлі `lib/bl/deep_links.dart` додайте логіку навігації для:
- `/app/*` - загальні посилання додатка
- `/lesson/*` - посилання на уроки
- `/profile/*` - посилання на профілі
- `/auth/*` - посилання автентифікації

## 🚨 Важливі моменти

1. **HTTPS обов'язково** - Deep links працюють тільки через HTTPS
2. **Домен повинен бути доступний** без редиректів
3. **Файли повинні віддаватися з правильним Content-Type**: `application/json`
4. **iOS потребує Team ID** в apple-app-site-association (вже додано: `PSWA65N6D2`)
5. **Android потребує SHA256 fingerprint** (вже додано)

## 📞 Підтримка

Якщо виникають проблеми:
1. Перевірте доступність файлів через браузер
2. Використайте [Apple App Site Association Validator](https://branch.io/resources/aasa-validator/)
3. Використайте [Android Asset Links Tester](https://developers.google.com/digital-asset-links/tools/generator)

## 🎉 Готово!

Після виконання всіх кроків ваші deep links будуть працювати через домен `empowermind.tech`!
