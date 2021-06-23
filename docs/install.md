# Install

>Get instructions to download and install UltraGen

## Instructions for all available systems

In this page you'll be guided to install UltraGen in your OS.

1. Download one of the versions presented here. We recommend you to use the latest stable. However, nighyly builds are also available.

1. Extract this zip in a path of your choice. Don't use a privileged path or you may have permissions problems while executing uploads or using sessions.

1. Set the **ULTRAGEN_HOME** environment variable to the place where you extracted UltraGen. It's required for UltraGen load some default modules.

1. Add the paths `%ULTRAGEN_HOME%\bin` in Windows or to `$ULTRAGEN_HOME/bin` to **PATH** environment variable. This step while optional may is really reaaly useful for running scripts just typing `ultragen` from any directory.

## Windows

- [UltraGen_Win64_0.0.6.zip](https://github.com/alantelles/ultragen/releases/download/0.6.0/UltraGen_Win64_0.0.6.zip)

## Linux

- [UltraGen_Linux64_0.0.6.zip](https://github.com/alantelles/ultragen/releases/download/0.6.0/UltraGen_Linux64_0.0.6.zip)

```callout
UltraGen for Linux was compiled with Ubuntu and is not tested with other distros. If you have any problem, please, let us know.:warning
callout
```
### Specific for Linux
    
UltraGen use a famous FreePascal project for serving its web pages. It's called [BrookFramework](https://github.com/risoflora/brookframework). However Brook uses a dynamic linked library to work. It's called [libsagui](https://github.com/risoflora/libsagui) from the same author [Silvio Clécio](https://github.com/silvioprog). It's a high-perfomance web server which you can use to deploy your application in production. For this, we need first add the path of the library to your OS configuration. The easiest way to do this is adding the path `ULTRAGEN_HOME/unix/libsagui-3.3.2/lib64` to your **$LD_LIBRARY_PATH** environment variable. This will enable applications using the `Brook` server in UltraGen.

Another caveat is that **libsagui** depends on your OS [glibc](https://en.wikipedia.org/wiki/GNU_C_Library) version. The version shipped with UltraGen is [3.3.2](https://github.com/risoflora/libsagui/releases/tag/v3.3.2) is expected to work with the **2.31** glibc version. If you need another version, please refer to [libsagui releases pages](https://github.com/risoflora/libsagui/releases) and find one suitable. The place where **libsagui** is hosted doesn't matter. You only must ensure that it's included in the dynamic library paths.

## Docker

Not surprisingly, the most compatible and easy way to run UltraGen is using the UltraGen docker image. You call pull the latest version or another image available on dockerhub. The versions are using CalVer for pre releases.


- Latest

    `docker pull alantelles/ultragen`

- Stable

    `docker pull alantelles/ultragen:06-22-pre`