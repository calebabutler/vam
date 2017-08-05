# vam
Vam is the simplest aur helper ever made. It is 55 lines of source code. That is so short, that on a computer with no internet connection, you can hand type the entire source code in less than 5 minutes. Sadly the program is useless on a computer with no internet connection. It has three options:

    vam -d # -> downloads aur packages and their aur dependencies
    vam -u # -> downloads aur updates and notifies the user of them
    vam -s # -> searches the aur through aur names and descriptions

Vam requires bash, git, jshon, curl, and gnu coreutils.

# Why use this instead of cower (auracle, or any other download-only aur helper)?

Cower/Auracle doesn't use git but tarballs, which has been deprecated since AUR 4. But also all of these aur helpers (in my opinion) just has too many gosh dang features. Cower is 1000 lines of C code. Why? I rewrote the functionality I used in 55 lines.

# How do you download it?

Before downloading it, it might be beneficial to understand how the aur works below, and maybe creating your own similar simple aur helper with maybe more features. If you don't want to make yet another AUR helper:

    # Download vam's aur package with git
    git clone https://aur.archlinux.org/vam.git
    # Go into the vam directory
    cd vam
    # make the package
    makepkg -si
    # do this command if you're moving to vam from an existing aur helper:
    vam -d $(pacman -Qm | awk '{print $1}')

# How does it work?

So the AUR switched to git. What does that mean? What benefit does it have for me? Well it makes downloading and updating from the command line a lot easier. Let's look at how to download from the AUR:

```shell
git clone https://aur.archlinux.org/$insert_package_name_here.git
```

Okay, so that's simple enough. But how do you download updates? Do you have to constantly keep track of the same package version numbers? Well, that's how it used to be for the most part. But now with git it's a lot simpler:

```shell
cd $insert_package_that_you_just_downloaded
git pull
```

Now this makes the AUR infinitely better to work with. If you ever need to download/update without an AUR helper, using straight git and a command line web browser like lynx will probably get you all the way there. However, you don't need text-based web browser to search the aur. You can also use the AUR's rpc interface, and that looks like this:

```shell
curl https://aur.archlinux.org/rpc/?v=5&type=search&arg=$insert_package_name_here
```

This will return a large JSON string with all of the results as long as extra information, such as descriptions and the popularity of each package. This is where the program jshon comes in a lot of handy. If we pipe the curl output (as well as silencing curl with -s) into jshon, we can only get the names of packages as results. Like so:

```shell
curl -s https://aur.archlinux.org/rpc/?v=5&type=search&arg=$insert_package_name_here | jshon -e results -a -e Name -u
```

Great. So now we can search, update, and download from the command line. But there's one more important command. Using the same rpc interface, we can also get information on a package, such as the dependencies. Info can be gotten with this command:

```shell
curl -g https://aur.archlinux.org/rpc/?v=5&type=info&arg[]=$insert_package_name_here
```

There you go! Now you can build your own AUR helper. Or not use any AUR helper at all. Or feel like this is all a waste of time and just use vam, cower, pacaur, yaourt, or whatever else.
