# Miscellanious `BASH` scripts

This repository contains a collection of BASH-scripts that can be installed to be used as commands in an Ubuntu distribution to make life easier. It was inspired by [this](https://github.com/ameinild/add-apt-key) repository, since I was looking for the best practices on adding new keys since apt-key was deprecated. However I needed an non-interactive script, so I decided to write my own.

So this repo was born, in which I will collect more useful BASH-scripts.

## Contents

- Repository contents
- Usage instructions
- Resources

## Repository Contents

A brief overview of the contents contained in this repository.

### Helper Script

- `apt-cmd-add`
  - Helper script to add the commands to bash

### APT Commands

- `apt-key-add`
  - Adds a new key signature to the keychain
  - Also able to automatically add corresponding repo
- `apt-src-add`
  - Adds a new source repository to sources.list.d

## Instructions

A description of how to use the various scripts and commands in this repository.

### Helper Script Usage

- Configure which commands to install in `apt-cmd-add.conf` by setting variables to `true` or `false`.
- Exectute using `sudo ./apt-cmd-add`.

### APT Commands Usage

#### apt-key-add

Usually you want to run this command by using:

```bash
apt-key-add 
-i=https://updates.signal.org/desktop/apt/keys.asc 
-o=signal-desktop 
-su='https://updates.signal.org/desktop/apt' 
-ss='xenial' 
-sc='main'
```

When the `-su`, `-ss` and `-sc` parameters are passed to the function, this call will also invoke `apt-src-add` and add the corresponding repository to `sources.list.d/`.

When issuing this command, the `-o` flag is optional to give it a distinct name, which is recommended in this specific case because the name `keys.asc` - which would be used otherwise - is rather non-descriptive.

For a more detailed overview of all the possibilities look inside inside the file itself or get it by using the help function:

- `apt-key-add -h`

or

- `apt-key-add --help`

#### apt-src-add

If you want to manually add a repository to the `sources.list.d/`, you would want to run this command by using:

```bash
apt-src-add 
-n=signal-desktop 
-u=https://updates.signal.org/desktop/apt 
-s=xenial 
-c=main 
-os=/usr/share/keyrings/signal-desktop-archive-keyring.gpg
```

For a detailed overview of all possibilities, look found inside the file itself, check the resources mentioned on the bottom of this README, or get it by using the help function:

- `apt-src-add -h`

or

- `apt-src-add --help`

The command is written to support all options from the RFC, however only the basic usage has been thorougly tested. Is  is able to output the new `DEB822` format (using `.sources`) as well as the older `OLF` (using `.list`) format files.

## Future work

### apt-add-src

- Add validation for all the options, as well as thouroughly test them. Currently only verified that the basic usage works, since most options will usually be left to their default values and should not be used in most use-cases.
- Automatically setup .bash_aliases.
## Resources

- [About the different .sources.d/ formats](https://repolib.readthedocs.io/en/latest/deb822-format.html)
- [Sources.list man pages](https://manpages.debian.org/stretch/apt/sources.list.5.en.html)
- [Bash redirection](https://web.archive.org/web/20230315225157/https://wiki.bash-hackers.org/howto/redirection_tutorial)