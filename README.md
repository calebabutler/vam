# yim
Yim is the simplest aur helper ever made. It is 52 lines of source code. That is so short, that on a computer with no internet connection, you can hand type the entire source code in less than 5 minutes. Sadly the program is useless on a computer with no internet. It has three options:

    yim -d # -> downloads aur packages and their aur dependencies
    yim -u # -> downloads aur updates and notifies the user
    yim -s # -> searches the aur through aur names and descriptions

Nam requires bash, git, jshon, and curl.

# Why use this instead of cower?

Cower doesn't use git but tarballs, which has been deprecated since AUR 4. But also cower just has too many gosh dang features. It is 1000 lines of C code. Why? When you can just rewrite the functionality you use in 52 lines. Plus it's also 5 letters instead of 3. If you're not convinced yet you're a lost cause.

# How do you download it?

Before you read how to download it, I recommend first understanding the entire program top to bottom. The explanation is right below here. After reading how it works, I recommend making your own yim-type aur helper with all of the features you need. If that sounds stupid:

    # Download nam's aur package with git
    git clone https://aur.archlinux.org/nam.git
    # Go into the nam directory
    cd nam-master
    # make the package
    makepkg -si
