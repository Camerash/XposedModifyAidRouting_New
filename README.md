# Xposed Module NFC AID Re-Routing

This is a repo based on [johnzweng's XposedModifyAidRouting](https://github.com/johnzweng/XposedModifyAidRouting)

Things changed:
- Project structure changed to gradle-based, Android Studio compatible (which is the main reason why I need to setup a new repo)
- Target SDK version to 27
- Fix android nfc class method not found bug (due to method refactored in Android 5.0 or above)
  - Target method `public AidResolveInfo resolveAidPrefix(String aid)` was changed to `public AidResolveInfo resolveAid(String aid)`, renders the old module useless
  - Compare Android sourcecode between [Android 4.4.4](https://android.googlesource.com/platform/packages/apps/Nfc/+/android-4.4.4_r2.0.1/src/com/android/nfc/cardemulation/RegisteredAidCache.java) and [Android 5.0.0](https://android.googlesource.com/platform/packages/apps/Nfc/+/android-5.0.0_r1/src/com/android/nfc/cardemulation/RegisteredAidCache.java)
  - Based on analysis in source code of class `HostEmulationManager.java` between [Android 4.4.4 line 171](https://android.googlesource.com/platform/packages/apps/Nfc/+/android-4.4.4_r2.0.1/src/com/android/nfc/cardemulation/HostEmulationManager.java#171) and [Android 5.0.0 line 160](https://android.googlesource.com/platform/packages/apps/Nfc/+/android-5.0.0_r1/src/com/android/nfc/cardemulation/HostEmulationManager.java#160), the new hooked method should be `resolveAid(String aid)`
