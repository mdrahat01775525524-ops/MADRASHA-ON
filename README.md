# MADRASHA-ON name: Build MADRASAH ONE APK

on:
  workflow_dispatch:
  push:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '17'

      - uses: android-actions/setup-android@v3

      - uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: '8.9'

      - name: Extract project
        run: unzip MADRASAH_ONE_Offline_Test_v1_1.zip -d project

      - name: Build APK
        run: |
          cd project/MadrasahOne_Test
          gradle assembleDebug

      - uses: actions/upload-artifact@v4
        with:
          name: MADRASAH-ONE-APK
          path: project/MadrasahOne_Test/app/build/outputs/apk/debug/app-debug.apk
