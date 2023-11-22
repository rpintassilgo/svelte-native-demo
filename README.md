# Svelte Native Demo

Small svelte native demo that contains a simple counter component and a simple colours game

## Initial Svelte Native setup with android environment

1. Install node
2. Install JDK version 8 or greater
3. Install Android Studio and configure ANDROID_HOME environment variable[^1]
4. Install NativeScript CLI globally
5. Run `ns doctor android` to verify the environment
6. You're good to go!

[^1]: This is an optional step, however it provides an easy-to-use interface for installing Android SDKs and an Android emulator.

For more information, check the official NativeScript documentation:  
[NativeScript Linux tutorial](https://docs.nativescript.org/setup/linux)
[NativeScript Windows tutorial](https://docs.nativescript.org/setup/windows)
[NativeScript MacOS tutorial](https://docs.nativescript.org/setup/macos)


## Create a new Svelte-Native app

After installing all the necessary tools and resources, create a new project
```bash
$ ns create myapp --svelte
$ cd myapp
```
Configure and start an Android emulator using Android Studio and run the app
```bash
$ ns run android
```

## Clone and try this demo

Install depencies and start
```bash
$ npm install
$ ns run android
```
\
Have fun with Svelte Native!
