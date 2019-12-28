**This document is intended for developers to compile with source code. For content that is not understood in the documentation or if you encounter an error, be sure to use Google Search.**

***

## 1.download the latest source code

```
git clone https://github.com/telegram-sms/telegram-sms.git telegram-sms
cd telegram-sms
git checkout nightly
```

## 2.configure the compilation environment

You can compile this project by referring to the compiled script shown in `.gitlab-ci.yml`

Configure environment variables, be careful to modify `ANDROID_HOME` for your `Android SDK` directory

```
export ANDROID_HOME=<Android SDK>
export KEYSTORE_PASSWORD=<Your password>
export ALIAS_PASSWORD=<Your password>
export ALIAS_NAME=<Your alias name>
export VERSION_CODE=1
export VERSION_NAME="Debug"
```

## 3.run compile

```
./gradlew assembleDebug
```

Or use the following command to generate the `release` version

```
./gradlew assembleRelease
```