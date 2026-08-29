# Fossify File Manager

<img alt="Logo" src="graphics/icon.webp" width="120" />

<a href='https://play.google.com/store/apps/details?id=org.fossify.filemanager'><img alt='Get it on Google Play' src='https://play.google.com/intl/en_us/badges/static/images/badges/en_badge_web_generic.png' height=80/></a> <a href="https://f-droid.org/packages/org.fossify.filemanager/"><img src="https://fdroid.gitlab.io/artwork/badge/get-it-on-en.svg" alt="Get it on F-Droid" height=80/></a> <a href="https://apt.izzysoft.de/fdroid/index/apk/org.fossify.filemanager"><img src="https://gitlab.com/IzzyOnDroid/repo/-/raw/master/assets/IzzyOnDroid.png" alt="Get it on IzzyOnDroid" height=80/></a>

Tired of file managers that slow you down and invade your privacy? Unlock a lightning-fast, secure, and completely customizable experience with Fossify File Manager. ⚡

**🚀 DOMINATE YOUR DIGITAL WORLD WITH BLAZING-FAST NAVIGATION:**
 - Swiftly manage your files with easy compression and transfer capabilities, keeping your digital life organized.
 - Quickly access your most-used folders with customizable home folder and favorite shortcuts.
 - Find what you need in seconds with intuitive navigation, search, and sorting options.

**🔐 FORTIFY YOUR DATA WITH UNPARALLELED PRIVACY AND SECURITY:**
 - Secure sensitive files with password, pattern, or fingerprint locks for hidden items or the entire app.
 - No internet access required – your files stay private and secure on your device.

**💾 MASTER YOUR STORAGE LIKE A PRO:**
 - Clear space with easy file and folder compression to maximize your device's potential.
 - Identify and clean up space-hogging files with the built-in storage analysis tool.
 - Seamlessly navigate root files, SD cards, and USB devices for total organization.

**📁 OPTIMIZE YOUR WORKFLOW WITH HANDY TOOLS:**
 - Create desktop shortcuts for instant access to your most-used files and folders.
 - Edit, print, or read documents easily with the light file editor, enhanced by zoom gestures.

**🌈 MAKE IT YOUR OWN WITH ENDLESS CUSTOMIZATION:**
 - Enjoy an ad-free, open-source experience that puts you in control, not corporate giants.
 - Personalize colors, themes, and icons to reflect your unique style and preferences.

Ditch the bloated, privacy-invading file managers and experience true freedom with Fossify File Manager. Download now and take back control of your digital life!

➡️ Explore more Fossify apps: https://www.fossify.org<br>
➡️ Open-Source Code: https://www.github.com/FossifyOrg<br>
➡️ Join the community on Reddit: https://www.reddit.com/r/Fossify<br>
➡️ Connect on Telegram: https://t.me/Fossify

<div align="center">
<img alt="App image" src="fastlane/metadata/android/en-US/images/phoneScreenshots/1_en-US.png" width="30%">
<img alt="App image" src="fastlane/metadata/android/en-US/images/phoneScreenshots/3_en-US.png" width="30%">
<img alt="App image" src="fastlane/metadata/android/en-US/images/phoneScreenshots/4_en-US.png" width="30%">
</div>
---

## Fork changes (Yet-Another-File-Manager)

- **Bugfix pass: investigated, no changes made.** ViewPager tabs
  (Files/Recents/Storage) use the same fresh-instance-per-scroll
  `PagerAdapter` pattern found in other Yet-Another apps, but this app
  registers no `EventBus` subscriptions, `BroadcastReceiver`s, or
  `ContentObserver`s in any of its fragments - confirmed by checking each
  one - so the leak found in Yet-Another-Voice-Recorder doesn't apply
  here; there's no global singleton holding a reference to an orphaned
  instance. File search (`ItemsFragment.searchQueryChanged()`) is properly
  backgrounded via `ensureBackgroundThread` and already has a stale-result
  guard (`lastSearchedText != text`) discarding out-of-order results from
  a superseded search - the same good pattern found in Messages'
  conversation search. Minor, not fixed: no debounce before starting a
  search, so rapid typing can start multiple concurrent background
  directory walks - a real but much smaller inefficiency than Contacts'
  original issue, since this doesn't block the UI thread the way a
  synchronous main-thread scan would. File deletion delegates to a shared
  Commons helper (`handleFileDeleting`), not custom logic in this app,
  so lower risk of an app-specific bug there.
