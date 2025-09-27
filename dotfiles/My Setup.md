# Nerd font setup in terminal

### Steps:
- Paste the font link address 
```
    wget -P ~/.local/share/fonts <https://github.com/ryanoasis/nerd-fonts/releases/download/v3.0.2/JetBrainsMono.zip>
```
- go to the fonts directory
```
    cd ~/.local/share/fonts
```
- unzip the font with this command
```
    unzip JetBrainsMono.zip
```
- remove the zip file
```
    rm JetBrainsMono.zip
```
-refresh the font cache
```
    fc-cache -fv
```

### If using default terminal, change the font to your font
### If using alacritty terminal or other change the config file and add font family as your font


# Neovim setup

- install neovim
```
    sudo apt install neovim
```
- make sure to not delete the nvim folder inside /usr/share folder
- if deleted then do this to remove neovim and install again
```
    sudo apt remove neovim

    // TODO: remove neovim from all the places and make sure to remove the cache as well, without this it will not work 
    rm -rf ~/.config/nvim
    rm -rf ~/.local/share/nvim
    rm -rf ~/.cache/nvim
```


# Lazyvim custom setup

- Put this in lazy.lua file
```
    -- import/override with your plugins
    {import = "lazyvim.plugins.extras.lang.json"},
    {import = "lazyvim.plugins.extras.lang.java"},
    {import = "lazyvim.plugins.extras.ui.mini-animate"},
```


- Put this in keymaps.lua file

```
    -- Open the Explore page with space pv
    vim.keymap.set("n", "<leader>pv", vim.cmd.Ex)

    vim.keymap.set('i', 'jf', '<Esc>', { noremap = true, silent = true })
    vim.keymap.set('i', 'fj', '<Esc>', { noremap = true, silent = true })
    vim.keymap.set('i', 'jh', '<Esc>', { noremap = true, silent = true })

    vim.opt.tabstop = 4
    vim.opt.softtabstop = 4
    vim.opt.shiftwidth = 4
    vim.opt.expandtab = true

```

# Brave browser suddenly stop launching
- Run this code 
```
rm ~/.config/BraveSoftware/Brave-Browser/SingletonLock
```
```
```

## change shortcut for switching desktops, alt + left or right
```
gsettings set org.gnome.desktop.wm.keybindings switch-to-workspace-left "['<Alt>Left']"
gsettings set org.gnome.desktop.wm.keybindings switch-to-workspace-right "['<Alt>Right']"
```

## change shortcut for switching desktops, alt + left or right square bracket
```
gsettings set org.gnome.desktop.wm.keybindings switch-to-workspace-left "['<Alt>bracketleft']"
gsettings set org.gnome.desktop.wm.keybindings switch-to-workspace-right "['<Alt>bracketright']"
```

## change shortcut for switching desktops, ctrl + left or right square bracket
```
gsettings set org.gnome.desktop.wm.keybindings switch-to-workspace-left "['<Control>bracketleft']"
gsettings set org.gnome.desktop.wm.keybindings switch-to-workspace-right "['<Control>bracketright']"
```


## change the shortcut to default, ctrl + alt + left or right
```
gsettings reset org.gnome.desktop.wm.keybindings switch-to-workspace-left
gsettings reset org.gnome.desktop.wm.keybindings switch-to-workspace-right
```


## Postman install
1. download the postman .tar file from the postman official website
2. extract it
3. create a desktop entry for it at /use/share/application
4. give the file path where you have extracted the file, (i store it in /home/softwares


## firefox UI change
download firefox from apt or move it to /home/subas/.mozilla/firefox
now go to firefox and search about:config
enable layout.css.moz-document.content.enabled and toolkit.legacyUserProfileCustomizations.stylesheets
now go to about:support and go to profile and open the directory
create a folder "chrome"
inside that create a file names "userChrome.css" --> for modification in the function
create another file "userContent.css" --> for modification in the home page like removing an element, styling an element etc
https://www.youtube.com/watch?v=aCdFs6rgeNI&t=212s
visit this youtube page to know more


## Open the grub menu
1.  open this file : 
	 ```
	  sudo vim /etc/default/grub 
	```
1. set the grub style to menu from hidden
2. and grub time to 10 
3. then run 
    ```
    sudo update-grub
	```
5. now restart and done


## Docker install in ubuntu

1. Visit docker official website [here](https://docs.docker.com/desktop/setup/install/linux/ubuntu/)
2. Download the .deb package
3. Install it using this command : 
	```
	sudo apt-get update
	sudo apt-get install ./docker-desktop-amd64.deb
	```
4. Now you have your docker desktop ready to use .

