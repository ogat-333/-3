# -3
Попытка 3
workflows:
  android-release:
    name: Гербарий Безымянного — Android Release
    environment:
      java: 17
    scripts:
      - name: Распаковать Android-проект
        script: |
          rm -rf buildsrc
          mkdir buildsrc
          unzip -q *.zip -d buildsrc
      - name: Собрать APK
        script: |
          PROJECT_DIR="$(dirname "$(find buildsrc -name settings.gradle -type f -print -quit)")"
          cd "$PROJECT_DIR"
          gradle --no-daemon assembleRelease
    artifacts:
      - buildsrc/**/app/build/outputs/apk/release/*.apk
