# App languages

The phone app supports eight languages in both the full and Play builds:

| Language | Locale | Resource folder |
| :-- | :-- | :-- |
| English | `en` | `values` (default and fallback) |
| 繁體中文 | `zh-Hant` | `values-b+zh+Hant` |
| 日本語 | `ja` | `values-ja` |
| 한국어 | `ko` | `values-ko` |
| 简体中文 | `zh-Hans` | `values-b+zh+Hans` |
| ไทย | `th` | `values-th` |
| Tiếng Việt | `vi` | `values-vi` |
| Deutsch | `de` | `values-de` |

## Choose a language

On Android 13 or newer, open the phone's **Settings > Apps > Clean Your TV > Language**.
Depending on the phone, this may be under **System > Languages > App languages**.
Choose one of the eight languages or follow the system language. The supported languages are
declared in `app/src/main/res/xml/locales_config.xml` and the application manifest.

On Android 9 through 12, the app follows the phone's system language. Change the preferred
language in the phone's settings, then reopen the app. Unsupported languages fall back to English.
Traditional Chinese covers Taiwan and Hong Kong, while Simplified Chinese covers China and
Singapore through Android's script matching.

No translation service, account, extra permission or internet connection is needed at runtime.
All text is packaged in the app. Android's system fonts provide fallback glyphs for scripts
outside the bundled Outfit typeface.

## Coverage and review

All 814 translatable resource entries in `app`, the six `feature` modules and `ui/design` have
seven localized counterparts. This covers connection instructions, setup, management, backup and
restore, add-ons, notifications and accessibility descriptions. English remains the source.
The new translations were machine-assisted, with terminology and key interface text edited;
native-speaker review and device layout checks are welcome before a production release.

Product names, package names, commands and licence identifiers retain their original spelling.
The bundled TV launcher and curtain are separately signed upstream APKs. Their text, the TV's
own settings, upstream module descriptions, diagnostic reports and this repository's website
are not translated by these phone-app resources. Their pins and signatures are unchanged.

## Maintain translations

- Add each new translatable entry to the matching locale folder in the same module.
- Preserve ICU argument names (`{tv}`, `{name}`), selector syntax (`plural`, `one`, `other`,
  `=0`), `#` count symbols, `spellout`, printf placeholders and `formatted="false"` attributes.
- Escape ASCII apostrophes and quotation marks for Android XML. XML-escape `&` and `<`.
- Keep shared resource names consistent across modules because Android merges their resources.
- Keep each `allow_body_emphasis_*` value an exact substring of `allow_body`.
- Use short control labels, check long German sentences and test with large fonts.

Run the offline resource checks:

```sh
python3 -m unittest discover -s scripts/tests -p test_localization.py -v
```

With JDK 21, the Android SDK and the pinned submodule available, run:

```sh
./gradlew check :app:assembleDebug
```

`LocalizationTest` resolves every translated string from the compiled resources on Android 9
and 15, formats ICU messages with several counts, checks argument names, verifies Chinese
regional matching and checks the English fallback. The localization workflow also uploads
debug APKs for both store flavours after a successful build.
