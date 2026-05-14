# plugins

This template project provides a collection of utilities and some parsers for convenient access to any content available on the web.

## Requirements

- Android Studio or IntelliJ IDEA (Community Edition is enough)
- Android SDK 35 or later (if not using IDE)
- Java 11 or later is required

## Usage

1. Open Terminal on root folder, build this project:

    On Linux & Unix system:
	```bash
	chmod +x gradlew && ./gradlew jar
 	```

    On Windows system:
    ```cmd
    .\gradlew.bat jar
    ```

2. Dex it with d8 after building:

	```bash
 	d8 --release build/libs/plugin.jar --output plugin.jar
 	```

**More simply, just run `buildJar` task in Android Studio / IntelliJ IDEA and dex it after building.**

## Credits

- Thanks to HOLOLIVE for providing free content on their official website.
- Thanks to [KotatsuApp](https://github.com/KotatsuApp) for providing HoloEarth parser and the core library.
- Thanks to [Keiyoushi](https://github.com/Keiyoushi) for providing Holonometria extensions code on GitHub.

### License

[![GNU GPLv3 Image](https://www.gnu.org/graphics/gplv3-127x51.png)](http://www.gnu.org/licenses/gpl-3.0.en.html)

<div align="left">

You may copy, distribute and modify the software as long as you track changes/dates in source files. Any modifications to or software including (via compiler) GPL-licensed code must also be made available under the GPL along with build & install instructions. See [LICENSE](./LICENSE) for more details.

</div>
