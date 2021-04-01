<p align="center"> <img src="https://upload.wikimedia.org/wikipedia/commons/5/5a/Animated_Wallpaper_Windows_10_-_Wallpaper_Engine.gif"></p>

## watermark_disabler
Disabling "Activate Windows" watermark made simple, the code in this repository is a PoC, and has not been tested above Windows 10 1803.

## how does this work?
The function responsible for drawing whole desktop including the watermark is xxxDesktopPaintCallback located in win32kfull.sys.
Both of the approaches used by this project were found while analyzing functions further down in the callstack.

## vcpkg :
vcpkg is a cross-platform command-line package manager for C and C++ libraries. It simplifies the acquisition and installation of third-party libraries on Windows, Linux, and macOS. If your project uses third-party libraries, we recommend that you use vcpkg to install them. vcpkg supports both open-source and proprietary libraries. All libraries in the vcpkg Windows catalog have been tested for compatibility with Visual Studio 2015, Visual Studio 2017, and Visual Studio 2019. Between the Windows and Linux/macOS catalogs, vcpkg now supports thousands of libraries. The C++ community adds more libraries to both catalogs on an ongoing basis.

- https://docs.microsoft.com/en-us/cpp/build/vcpkg?view=msvc-160

- https://stackoverflow.com/questions/60245518/get-vcpkg-to-include-the-vcpkg-include-directory-in-the-include-path-when-buildi


<p align="center"> <a href="https://www.buymeacoffee.com/tahiri" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/lato-orange.png" alt="Buy Me A Coffee" style="height: 51px !important;width: 217px !important;" ></a> <p>
<p align="center">
    <a href="https://yassertahiri.medium.com/">
    <img alt="Medium" src="https://img.shields.io/badge/Medium%20-%23000000.svg?&style=for-the-badge&logo=Medium&logoColor=white"/></a>
    <a href="https://twitter.com/THyasser1">
    <img alt="Twitter" src="https://img.shields.io/badge/Twitter%20-%231DA1F2.svg?&style=for-the-badge&logo=Twitter&logoColor=white"</a>
    <a href="https://discord.gg/crNvkTYPYG">
    <img alt="Discord" src="https://img.shields.io/badge/Discord%20-%237289DA.svg?&style=for-the-badge&logo=discord&logoColor=white"/></a>
</p>
