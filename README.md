# Ninja Customer Mobile App

## Table of Contents
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [Development](#development)
- [Running Production On Staging Build](#release-production-build)
- [Staging Build](#staging-build)
- [Release Production Build](#release-production-build)
- [Add a New npm Package with Native Code](#add-a-new-npm-package-with-native-code)
- [Add a New Device to Development](#add-a-new-device-to-development)
- [Patch Details](#patch-details)
- [Refactor Roadmap](#refactor-roadmap)
  - [Separate the UI from the Logic](#separate-the-ui-from-the-logic)
  - [Move All API Calls and Formatting to Services](#move-all-api-calls-and-formatting-to-services)
  - [Gradually Remove All Legacy Code](#gradually-remove-all-legacy-code)
- [Fastlane](#fastlane)
- [How to Run on Production](#how-to-run-on-production)
- [CodePush](#codepush)
- [Language Support](#language-support)
- [Theme Pattern](#theme-pattern)
  - [Sizes](#sizes)
  - [Colors](#colors)
  - [TextStyle](#textstyle)
  - [Icons](#icons)
 
## Getting Started
 
### Prerequisites
 
Before you begin, ensure you have met the following requirements:
 
- You have installed Node.js (which includes npm).
- You have installed Yarn.
- You have installed Watchman.
 
For iOS development:
- You have a Mac with the latest version of macOS.
- You have Xcode installed from the Mac App Store.
- You have installed CocoaPods:
    ```sh
    sudo gem install cocoapods
    ```
 
For Android development:
- You have installed Android Studio.
- You have set up your Android development environment by following the React Native documentation.
 
### Installation
 
To set up the project locally, follow these steps:
 
Clone the repository:
```sh
git clone https://github.com/ananinja/customer-app.git
cd customer-app
```
 
Install JavaScript dependencies:
```sh
yarn install
```
 
For iOS, install the necessary pods:
```sh
cd ios && bundle exec pod install
```
 
Start the Metro Bundler:
```sh
yarn start
```
 
Run the app:
 
For iOS:
```sh
yarn ios
```
 
For Android:
```sh
yarn android
```
 
## Development
 
To set up the development environment and run the app locally, follow these steps:
 
Navigate to the iOS directory and install necessary pods:
```sh
cd ios && pod install && fastlane development
```
 
Install JavaScript dependencies:
```sh
yarn install
```
 
Run the app on an iOS simulator:
```sh
yarn ios
```
 
## Running Production On Staging Build 
 
To run the production environment on staging build, uncomment line 16 in `AppInfo.ts` like this:
```ts
return appEnv;
```
 
## Staging Build
 
To build a staging version of the app, use the following commands:
 
Navigate to the iOS directory:
```sh
cd ios
```
 
Use Fastlane to build the production version:
```sh
fastlane development
```
 
## Release Production Build
 
To build and release a production version of the app, use the following commands:
 
Navigate to the iOS directory:
```sh
cd ios
```
 
Use Fastlane to build the production version:
```sh
fastlane production
```
 
## Add a New npm Package with Native Code
 
To add a new npm package that includes native code, follow these steps:
 
Add the package using Yarn:
```sh
yarn add PACKAGE_NAME
```
 
Navigate to the iOS directory and install necessary pods:
```sh
cd ios && bundle exec pod install
```
 
After adding the package, bump the minor version of `CFBundleShortVersionString` in `Info.plist`. For example, update the version from 1.56.678 to 1.57.678.
 
## Add a New Device to Development
 
To register a new device for development, use the following Fastlane command:
```sh
fastlane run register_device udid:"20b0db064139fb61843d1e58c4b9a41ab6698621" name:"My iPhone"
```
 
## Patch Details**
 
For detailed information on patches, please refer to the patch page.
 
## Refactor Roadmap
 
## Separate the UI from the Logic:
- Extract UI components to their own files, separating them from logic and styles.
- Minimize file length by creating custom hooks, styles, and dedicated logic files.
 
## Move All API Calls and Formatting to Services:
- Create dedicated services like CatalogService, OrdersService, and PaymentService to handle API calls, data formatting, and caching.
 
## How We Call APIs
- All API calls are handled through a centralized file located at `src/Services/ApiClient/index.ts`. This file provides a single point of entry for all network requests, ensuring a consistent approach to error handling, request formatting, and response processing.
 
## Gradually Remove All Legacy Code:
- Identify and refactor or remove outdated code to improve maintainability and performance.
 
## Fastlane
 
Fastlane is used to automate the build and release process for both development and production environments. Ensure you have Fastlane installed and configured correctly before running the commands.
 
## How to Run on Production
 
To run the app in a production environment, build the production version and deploy the assets using the previously mentioned commands under "Release Production Build" and "Release Production Assets."
 
## CodePush
 
CodePush allows for the deployment of app updates directly to users' devices. Ensure you have set up CodePush correctly by following the instructions in the official CodePush documentation.
 
We need to make sure that with staging we need to send staging CodePush and with production we need to send production CodePush.
 
## How Staging and Production CodePush Triggers
- Merging with the staging branch triggers staging CodePush.
- Merging with the main branch triggers production CodePush.
- We can upload CodePush manually with any branch and any production or staging environment.
 
## Language Support
 
This app supports two locales: English and Arabic. We use the `i18n-js` module for localization. Developers only need to add strings to the `en.json` file. GitHub Actions will push these changes to Localazy, and the marketing team will manage the `ar.json` file.
 
## Theme Pattern
 
### Sizes
 
The `Sizes.ts` file defines padding and margin sizes for various elements. It is structured to provide a consistent spacing system throughout the app.
```ts
import { StyleSheet } from 'react-native';
 
export const Sizes = StyleSheet.create({
  // Padding
  'p-2': { padding: 2 },
  'p-4': { padding: 4 },
  // ... more padding sizes
 
  // PaddingStart
  'ps-2': { paddingStart: 2 },
  'ps-4': { paddingStart: 4 },
  // ... more paddingStart sizes
 
  // PaddingEnd
  'pe-2': { paddingEnd: 2 },
  'pe-4': { paddingEnd: 4 },
  // ... more paddingEnd sizes
 
  // PaddingTop
  'pt-2': { paddingTop: 2 },
  'pt-4': { paddingTop: 4 },
  // ... more paddingTop sizes
 
  // PaddingBottom
  'pb-2': { paddingBottom: 2 },
  'pb-4': { paddingBottom: 4 },
  // ... more paddingBottom sizes
 
  // PaddingVertical
  'py-2': { paddingVertical: 2 },
  'py-4': { paddingVertical: 4 },
  // ... more paddingVertical sizes
 
  // PaddingHorizontal
  'px-2': { paddingHorizontal: 2 },
  'px-4': { paddingHorizontal: 4 },
  // ... more paddingHorizontal sizes
 
  // Margin
  'm-2': { margin: 2 },
  'm-4': { margin: 4 },
  // ... more margin sizes
 
  // MarginStart
  'ms-2': { marginStart: 2 },
  'ms-4': { marginStart: 4 },
  // ... more marginStart sizes
 
  // MarginEnd
  'me-2': { marginEnd: 2 },
  'me-4': { marginEnd: 4 },
  // ... more marginEnd sizes
 
  // MarginTop
  'mt-2': { marginTop: 2 },
  'mt-4': { marginTop: 4 },
  // ... more marginTop sizes
 
  // MarginBottom
  'mb-2': { marginBottom: 2 },
  'mb-4': { marginBottom: 4 },
  // ... more marginBottom sizes
 
  // MarginVertical
  'my-2': { marginVertical: 2 },
  'my-4': { marginVertical: 4 },
  // ... more marginVertical sizes
 
  // MarginHorizontal
  'mx-2': { marginHorizontal: 2 },
  'mx-4': { marginHorizontal: 4 },
  // ... more marginHorizontal sizes
});
```
 
### Usage
 
Import the `Sizes` object and use it in your component styles:
```ts
import { Sizes } from './path/to/Sizes';
 
// Example usage in a component
const styles = StyleSheet.create({
  container: {
    ...Sizes['p-10'],  // Padding of 10
    ...Sizes['m-20'],  // Margin of 20
  },
});
```
 
### Colors 
 
The `Colors.ts` file defines a comprehensive palette of colors for the application. The colors are grouped by themes and usage contexts to maintain a cohesive design.
 
### Base Colors
 
These are fundamental colors used across different themes.
```ts
const BASE_COLORS = {
  Base: {
    Black: '#000000',
    White: '#ffffff',
    NinjaPremium: '#033837',
    NinjaPremiumOrange: '#ff900a',
    NinjaPremiumLight: '#f6ffff',
  },
  // Other color groups (Ninja, Coffee, Cool
 
gray, etc.)
};
```
 
### Extended Colors
 
These colors are derived from the base colors and are categorized by usage context.
```ts
export const COLORS = {
  ...BASE_COLORS,
  Border: {
    Primary: BASE_COLORS.Coolgray[300],
    // Other border colors
  },
  Text: {
    Primary: BASE_COLORS.Coolgray[800],
    // Other text colors
  },
  Frame: {
    Primary: BASE_COLORS.Base.White,
    // Other frame colors
  },
  TransparentBlack: {
    '04': 'rgba(0, 0, 0, 0.04)',
    // Other transparent black colors
  },
};
```
 
### Usage 
 
Import the `COLORS` object and use it in your component styles:
```ts
import { COLORS } from './path/to/Colors';
 
// Example usage in a component
const styles = StyleSheet.create({
  text: {
    color: COLORS.Text.Primary,  // Primary text color
  },
  border: {
    borderColor: COLORS.Border.Primary,  // Primary border color
  },
});
```
 
### TextStyle
 
We define text styles and font-related properties in a dedicated file `theme.ts`. We have a separate component for Text named `TextV2` for consistency in the design of our text. Make sure to use the same component throughout the app.
 
### Usage 
```ts
<TextV2></TextV2>
```
 
### Icons
 
Similar to Text, we use the `IconV2` component for consistency in the Icons. To use the icons, add icons to the `src/Assets` folder and run the following:
```sh
yarn icon:svg
```
 
## Usage
```ts
<IconV2
  name="Plus"
  size={20}
  color={COLORS.Base.Black}
/>
```
