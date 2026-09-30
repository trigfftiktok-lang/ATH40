# M3SB APON SDK integration

The project uses the M3SB APON iOS SDK **v1.1.0** (Signature v3) in `ThreeOneOSFive/helpers/APONLicenseSDK.swift`. The v1.1 client sends the runtime dylib count and names with `/api/sdk/verify` and `/api/sdk/check`, so the API can apply the package's configured injection policy. The app fails closed for patch application until a fresh server response explicitly returns `allow_inject: true`; restore operations remain available.

The project already has its own Swift license screen and activation flow, so this integration uses the SDK's Swift layer. Do not add `APONGate.m` from the vendor archive: it contains hard-coded credentials and imports an `APONGate.h` file that is not included. The Swift integration avoids that unsafe/incomplete Objective-C gate and uses the app's existing activation UI.

## Private credentials

Do **not** commit package credentials. `Info.plist` now reads `APON_PACKAGE_TOKEN` and `APON_HMAC_SECRET` from Xcode build settings; the values are not stored in this source tree.

### Local macOS build

```bash
export APON_PACKAGE_TOKEN='(set privately from the API owner)'
export APON_HMAC_SECRET='(set privately from the API owner)'
./build_unsigned.sh
```

### GitHub Actions

Add repository Actions secrets named `APON_PACKAGE_TOKEN` and `APON_HMAC_SECRET`, using the latest owner-generated values from the private `M3SB_API_Config.json` fields `token` and `hmac_secret`. Replace the previous secret values when switching to package ID 130. Never commit `M3SB_API_Config.json` or paste either value into chat. The `build.yml` and `build-api-ipa.yml` workflows pass the secrets to Xcode without writing them to the repository.

The latest owner-generated configuration is for `ATH IPA` (package ID 130) and bundle ID `com.apple.mobile.MobileHouseArrest`. Keep the bundle ID and package configuration aligned with the API owner's dashboard. The API remains authoritative for license status and whether injection is allowed.

## Build validation

Build on macOS with Xcode. This sandbox is Linux and does not include `xcodebuild`, so the archive/IPA must be compiled and tested on macOS. A successful unsigned build still needs to be signed using the intended authorized deployment method before installation.
