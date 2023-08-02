# makedeb

Script for building Debian package quickly and easily. Inspired by Archlinux's makepkg.

## Example

Check the `DEBBUILD`

## Reference

### Build process

First it download needed content from array `sources`, then use function `pkgver` to determine the package version, then run function `build` and function `package`, then run hooks `debian_(pre|post)(inst|rm)` and make the printed strings as debian's hook scripts. Finally generate .deb with files in `$pkgdir`.

### Download and extract source

Every string in array `source` should be like `<actual_file_name>::<download_url>`. When downloading, the `download_url` content will be named with `<actual_file_name>`. When `build` and `pacage` run, every `<actual_file_name>` will be copied to `$srcdir`. If the file is a compressed file, it will be decompressed, if the file is a git repo, the specific branch, commit or tag will be checkouted.

### Global variables

- `pkgname`: package's name
- `pkgver`: package's version, if need to extract version from source, use function `pkgver`
- `pkgrel`: debian package reference, it should increase by one every build
- `pkgdesc`: package's description
- `section`: default `misc` if not specified
- `priority`: default `optional` if not specified
- `url`: packages upstream url
- `maintainer`: maintainer's contect information

### Global functions

- `pkgver`: should print the actual version. This override the variable `pkgver`
- `build`: do something like compile source
- `package`: do something like copy file from `$srcdir` to `$pkgdir`
- `debian_(pre|post)(inst|rm)`: should print content of debian hooks file
