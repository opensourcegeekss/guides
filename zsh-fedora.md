# Install ZSH Shell -

Guide to install ZSH shell and plugins on ubuntu and fedora.

## Requirements -

```bash
# For fedora or RedHat based distros -
sudo dnf install -y git zsh wget powerline-fonts
sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

## Install plugins -

```bash
# 1. zsh-autosuggestions -
git clone https://github.com/zsh-users/zsh-autosuggestions \
${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# 2. zsh-syntax-highlighting -
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git \
${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

# 3. zsh-history-substring-search -
 git clone https://github.com/zsh-users/zsh-history-substring-search \
 ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-history-substring-search
```

After installing [clonning] plugins you\`ll need to enable them in your `.zshrc` file.

```bash
# Open your .zshrc file and find folling line -
plugins=(git)

# Replace it with following line -
plugins=(git zsh-autosuggestions zsh-syntax-highlighting zsh-history-substring-search)
```

Note - To get hidden .zshrc file, press CTRL + H to show hidden files

## Install theme/prompt -

To use custom prompt you`ll need to install supported font and needs to set as default font for your terminal.

>It`s optional for Ubuntu/Debian based users.

[Click here to download powerlevel10k fonts](https://github.com/romkatv/powerlevel10k?tab=readme-ov-file#fonts)

> You can visit powerlevel10k github repo for the same

```bash
# Install fonts -
# Copy your downloaded fonts to following directory
# If directory is not present use following command
mkdir -p ~/.local/share/fonts
cp ~/Downloads/*.ttf ~/.local/share/fonts/
sudo fc-cache -fv

# powerlevel10k theme -
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git \
${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

# Open your .zshrc file and find folling line -
ZSH_THEME="robbyrussell"

# Replace it with following line -
ZSH_THEME="powerlevel10k/powerlevel10k"
```

Save file and reopen your terminal or do `source ~/.zshrc` and follow instructions to enable new prompt.
