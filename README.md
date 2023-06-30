# Experimental Fortran/C interfaces

This repository contains **experimental** Fortran bindings for various C libraries, automatically generated with the [cfwrapper](https://github.com/vmagnin/gtk-fortran/wiki/How-to-hack-the-cfwrapper) program of the gtk-fortran project. **Do not use for production.** The objective is just to offer raw files to test, which could possibly lead up to the creation of new Fortran libraries.

These interfaces are not 100% complete but if you have written a proof of concept and want to go further, I can try to improve the behavior of the cfwrapper. You can also write by hand the possibly missing crucial interfaces.

These files are under the very flexible [MIT license](https://mit-license.org/). They can therefore be included into a project using another license.

## List of libraries interfaces

- `src/libsoup3/` (HTTP client/server library): generated from `libsoup3-devel` 3.4.2 in Fedora 38. See the [Soup 3.0 documentation](https://libsoup.org/libsoup-3.0/index.html).

- `src/libadwaita/` (Building blocks for modern GNOME applications): generated from `libadwaita-devel` 1.3.3 in Fedora 38. See the [Adwaita documentation](https://gnome.pages.gitlab.gnome.org/libadwaita/doc/).

### List of the files for each library

For each library you will find a batch of files (only the two first files are absolutely needed):

- `\*-auto.f90`: the Fortran module with the interfaces.
- `other_enums-auto.in`: a file with the enums that is included in the module with an `include` statement.
- `interfaces_index.csv`: the list of the generated interfaces.
- `interfaces_types.csv`: the C types used by the cfwrapper.
- `interfaces_funptr.csv`: the function pointers used by the cfwrapper.
- `*.txt`: the statistics output by the cfwrapper.
- `cfwrapper-errors.csv`: useful to understand the problems encountered by the wrapper.

## Requirements and dependencies

You need:

* a modern Fortran compiler, for example GFortran or the Intel ifort/ifx compilers. See the [Fortran-lang.org compilers page](https://fortran-lang.org/compilers/) for other compilers.
* The development files of the libraries.
* (optional) The Fortran Package Manager [fpm](https://fpm.fortran-lang.org/). But fpm is optional: you can also just copy the two `.f90` and `.in` files in the directory of your project.

### Installation in Linux

If you have a GitHub account, just clone the repository:

```
$ git clone git@github.com:vmagnin/experimental_interfaces.git
$ cd experimental_interfaces
```

and install the dev files of the library you want to explore.

### Installation in Windows

You can use for example the [MSYS2](http://www.msys2.org/) environment:

* https://packages.msys2.org/base/mingw-w64-cairo
* https://packages.msys2.org/base/mingw-w64-fpm

Install the following packages via the MSYS2-MSYS shell:

  * build tools: 
    * `$ pacman -S mingw-w64-ucrt-x86_64-toolchain base-devel` (it will install gcc, gdb, gfortran, python, make, pkgconf...)
  * git: 
    * `$ pacman -S git`
  * Fortran Package Manager fpm: 
    * `$ pacman -S mingw-w64-ucrt-x86_64-fpm`

and the libraries you want to explore. Then start the MSYS2-UCRT64 shell.

If you have a GitHub account, just clone the repository:

```
$ git clone git@github.com:vmagnin/experimental_interfaces.git
$ cd experimental_interfaces
```

## Testing

```bash
$ fpm test
```

## fpm

To use these interfaces in a fpm project, add the following section to your project `fpm.toml` file:

```toml
[dependencies]
experimental_interfaces = {git = "https://github.com/vmagnin/experimental_interfaces" }
```
