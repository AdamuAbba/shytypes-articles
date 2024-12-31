repo: [flash-mobile](https://github.com/lnflash/flash-mobile)

- [x] Clone and setup
- [x] setup ruby and cocoads
- [] run on IOS
> [!bug]
>
>
> ```json
>yarn run v1.22.22
>warning ../../package.json: No license field
>$ react-native run-ios
info Found Xcode workspace "LNFlash.xcworkspace"
info Found booted iPhone 16 Pro
info Launching iPhone 16 Pro
info Building (using "xcodebuild -workspace LNFlash.xcworkspace -configuration Debug -scheme LNFlash -destination id=97F983ED-47A8-455A-B893-7B261CFE0A06")
Run script build phase 'Bundle React Native code and images' will be run during every build because it does not specify any outputs. To address this issue, either add output dependencies to the script phase, or configure it to run in every build by unchecking "Based on dependency analysis" in the script phase. (in target 'LNFlash' from project 'LNFlash')
Run script build phase 'Start Packager' will be run during every build because it does not specify any outputs. To address this issue, either add output dependencies to the script phase, or configure it to run in every build by unchecking "Based on dependency analysis" in the script phase. (in target 'LNFlash' from project 'LNFlash')
Run script build phase 'Run Script' will be run during every build because it does not specify any outputs. To address this issue, either add output dependencies to the script phase, or configure it to run in every build by unchecking "Based on dependency analysis" in the script phase. (in target 'LNFlash' from project 'LNFlash')
>
Run script build phase '[CP-User] [RNFB] Crashlytics Configuration' will be run during every build because it does not specify any outputs. To address this issue, either add output dependencies to the script phase, or configure it to run in every build by unchecking "Based on dependency analysis" in the script phase. (in target 'LNFlash' from project 'LNFlash')
Run script build phase '[CP-User] [RNFB] Core Configuration' will be run during every build because it does not specify any outputs. To address this issue, either add output dependencies to the script phase, or configure it to run in every build by unchecking "Based on dependency analysis" in the script phase. (in target 'LNFlash' from project 'LNFlash')
>
info 💡 Tip: Make sure that you have set up your development environment correctly, by running react-native doctor. To read more about doctor command visit: https://github.com/react-native-community/cli/blob/main/packages/cli-doctor/README.md#doctor
>
error Failed to build iOS project. We ran "xcodebuild" command but it exited with error code 65. To debug build logs further, consider building your app with Xcode.app, by opening LNFlash.xcworkspace.
error Command failed with exit code 1.
info Visit https://yarnpkg.com/en/docs/cli/run for documentation about this command.
> ```
- [x] run on android
