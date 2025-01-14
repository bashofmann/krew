---
title: Installing
slug: install
weight: 200
---

Krew itself is a `kubectl` plugin that is installed and updated via Krew (yes,
Krew self-hosts).

> ⚠️ **Warning:** krew is only compatible with `kubectl` v1.12 or later.

- **macOS/Linux**: [bash/zsh](#bash), [fish](#fish)
- **[Windows](#windows)**

## macOS/Linux {#posix}

#### Bash or ZSH shells {#bash}

1. Make sure that `git` is installed.
1. Run this command to download and install `krew`:

    ```sh
    (
      set -x; cd "$(mktemp -d)" &&
      curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/krew.tar.gz" &&
      tar zxvf krew.tar.gz &&
      KREW=./krew-"$(uname | tr '[:upper:]' '[:lower:]')_$(uname -m | sed -e 's/x86_64/amd64/' -e 's/arm.*$/arm/' -e 's/aarch64$/arm64/')" &&
      "$KREW" install krew
    )
    ```

1. Add the `$HOME/.krew/bin` directory to your PATH environment variable. To do
   this, update your `.bashrc` or `.zshrc` file and append the following line:

     ```sh
     export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"
     ```

   and restart your shell.

1. Run `kubectl krew` to check the installation.

#### Fish shell {#fish}

1. Make sure that `git` is installed.
1. Run this command in your terminal to download and install `krew`:

    ```fish
    begin
      set -x; set temp_dir (mktemp -d); cd "$temp_dir" &&
      curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/krew.tar.gz" &&
      tar zxvf krew.tar.gz &&
      set KREWNAME krew-(uname | tr '[:upper:]' '[:lower:]')_(uname -m | sed -e 's/x86_64/amd64/' -e 's/arm.*$/arm/' -e 's/aarch64$/arm64/' ) &&
      ./$KREWNAME install krew &&
      set -e KREWNAME; set -e temp_dir
    end
    ```

1. Add the `$HOME/.krew/bin` directory to your PATH environment variable. To do
   this, update your `config.fish` file and append the following line:

     ```fish
     set -gx PATH $PATH $HOME/.krew/bin
     ```

   and restart your shell.

1. Run `kubectl krew` to check the installation.

## Windows {#windows}

1. Make sure `git` is installed.
1. Download `krew.exe` from the [Releases][releases] page to a directory.
1. Launch a command prompt (`cmd.exe`) with administrator privileges (since the installation requires use of symbolic links) and navigate to that directory.
1. Run the following command to install krew:

    ```sh
    krew install krew
    ```

1. Add the `%USERPROFILE%\.krew\bin` directory to your `PATH` environment variable
   ([how?](https://java.com/en/download/help/path.xml))

1. Launch a new command-line window.
1. Run `kubectl krew` to check the installation.

[releases]: https://github.com/kubernetes-sigs/krew/releases

## Other package managers

You can alternatively install Krew via some OS-package managers like Homebrew
(macOS).

However, that method is not actively supported at this time.
