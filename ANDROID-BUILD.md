# Android-only build

This copy contains only the Android application target. Desktop JVM, iOS, and their packaging configuration have been removed.

## GitHub Actions

Open **Actions → Build Android APK → Run workflow**. The APK is uploaded as the `TEFManager-Android` artifact.

The workflow builds without any signing secret. In that case Gradle uses the automatically generated Android debug keystore, so the previous `Failed to read key TEFManager from store` error is avoided.

For a stable release signature, add these repository secrets from the original valid keystore:

- `KEYSTORE_BASE64`: Base64 contents of the `.p12` or `.jks` file
- `KEYSTORE_PASSWORD`
- `KEY_ALIAS`
- `KEY_PASSWORD`

The workflow validates the keystore first. If it cannot be opened, it falls back to the generated debug keystore.

## Important

An APK signed with the generated debug key cannot update an APK signed with a different key. Uninstall the old TEFManager first, or provide the original release keystore to keep the same signature.
