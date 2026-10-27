# Multilingual fork releases

This fork publishes the signed full-flavour Android APK at
<https://github.com/TonyBinheWu/cleanyourtv-app/releases>.
The latest published fork version is **0.3.4.1**, version code **8**, tag **multilingual-0.3.4.1**, based on upstream 0.3.4. The first fork release was 0.3.3.1 (7).
The source branches are now synchronized with upstream **0.4.0**, commit `e42aaf2`, and include
1,066 translatable resource entries in all sixteen languages. A source synchronization does not
replace an existing Release asset. Published APKs retain the version shown on their Release page.
It includes English, Traditional Chinese, Japanese, Korean, Simplified Chinese, Thai, Vietnamese
and German, plus Hindi, Spanish, French, Modern Standard Arabic, Bengali, Russian, Portuguese and Indonesian. The full build's update check points to this fork's latest release.

## Install and update

Download the APK asset from the Release and allow your browser or file manager to install it.
Android 9 or newer is required. Android 13+ offers per-app language settings; Android 9–12 follows
the phone's language. The English default remains available offline.

This APK is a release build with R8 and resource shrinking, not a debuggable build. Every APK in
this fork's release line must use the same fork signing key and a larger version code, so a future
release can update an existing fork installation without uninstalling it.

The fork uses the upstream application ID (`tv.cleanyour.app`) with its own signing certificate.
Android cannot install it over the original author's APK, or a Debug APK signed with a different
key. Before removing such an installation, export any restore-point copies you need. Uninstalling
the existing app deletes its local records and restore points. Removing the phone app does not
undo changes already made to a TV. No shared signing identity with the upstream project is claimed.

The public fork certificate fingerprint is in `fork-release-signer.sha256`; each Release includes
an APK checksum and signature-verification report. Private signing material is never committed.
The signing store and password were also retained locally under the task's private work files.
Preserve them and the repository signing secrets for future updates. Never attach them to a Release.

## Build another signed APK

Run **Actions > fork-signed-apk > Run workflow**. It reads the encrypted repository secrets
`CYT_FORK_KEYSTORE_BASE64` and `CYT_FORK_KEYSTORE_PASSWORD`, builds the full Release APK, runs
`check` and the size gate, verifies the v2/v3 signature and certificate, checks that the APK is
not debuggable and contains the requested languages, then uploads the signed artifact.

For the next release, use the version name and code in `app/build.gradle.kts` (a higher code than
the previous published APK) and a matching `multilingual-<version>`
tag. Run the workflow, inspect the successful result, then attach its verified APK and checksums
to a GitHub Release with notes. The `multilingual-` prefix avoids the upstream `v*` release pipeline,
which expects the original maintainer's offline signing key.
The signing workflow reads the synchronized app version automatically; its checks and APK name
do not need a separate version edit.

The upstream contribution lives separately in branch `i18n-eight-languages` and
[PR #271](https://github.com/udhaykumarbala/cleanyourtv-app/pull/271). Update that branch to add
translation improvements to the same PR. Fork signing, version numbering and update URLs are
excluded from the upstream contribution. The original author decides whether to merge it.
