# arch-pkgbuild

This repo contains `PKGBUILD`s for several of the software I use, that is not available on the **Official Arch Repositories**.  These `PKGBUILD`s' `*.pkg.tar.zst` will probably be added to [BreadFactory-repo](https://github.com/Nojjia/BreadFactory-repo).

## Packages

Packages are available through branches.

List of packages:
- [dwm](https://github.com/Nojjia/arch-pkgbuild/tree/dwm)
- [zen-browser-git](https://github.com/Nojjia/arch-pkgbuild/tree/zen-browser)
- [zen-browser-bin](https://github.com/Nojjia/arch-pkgbuild/tree/zen-browser-bin)
<!-- - [arduino-ide](https://github.com/Nojjia/arch-pkgbuild/tree/arduino-ide-bin)-->

My idea is that, if I need to build a specific PKGBUILD(for whatever reason), I'll just run `git clone https://github.com/Nojjia/arch-pkgbuild.git --branch=XYZ`, `XYZ` being the branch.

## Package testing and sanity checks - Reminder for me

1. `makepkg`

2. `pacman -Qpl pkgname.pkg.tar.zst`

3. `pacman -Qpi pkgname.pkg.tar.zst`

4. `namcap PKGBUILD`

5. `namcap pkgname.pkg.tar.zst`

6. `pkgctl build`
