---
category: ci
confidence: low
documentType: how-to
scope: org
contentHash: 0b5201932d71
tags: [release]
source: README.md
verified: 2026-07-16
---

## Download a binary

The pre-compiled binaries can be downloaded from [release page](https://github.com/appleboy/gorush/releases).

With `Go` installed

```sh
go get -u -v github.com/appleboy/gorush
```

On linux

```sh
wget https://github.com/appleboy/gorush/releases/download/v1.14.0/gorush-v1.14.0-linux-amd64 -O gorush
```

On OS X

```sh
wget https://github.com/appleboy/gorush/releases/download/v1.14.0/gorush-v1.14.0-darwin-amd64 -O gorush
```

On Windows

```sh
wget https://github.com/appleboy/gorush/releases/download/v1.14.0/gorush-v1.14.0-windows-amd64.exe -O gorush.exe
```

On macOS, use Homebrew.

```sh
brew install --HEAD https://github.com/appleboy/gorush/raw/master/HomebrewFormula/gorush.rb
```

## See Also
- [build gorush binary](../build/build-gorush-binary.md) <!-- rel:strong -->
- [memory usage](../tests/memory-usage.md) <!-- rel:related -->
- [install from source](../code-conventions/git/install-from-source.md) <!-- rel:related -->
- [ios example](../security/ios-example.md) <!-- rel:weak -->
- [features](../observability/alerting/features.md) <!-- rel:weak -->
