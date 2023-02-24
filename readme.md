Development Environment Setup
===

# Overview

When getting on a new machine, development container, or virtual machine, 
there are several things I miss that I usually have configured in my Linux 
development environment. This setup, though simple, takes time and effort
and it really should be automated. 

This repository contains some configuration files for some of the tools I
commonly use. To use it, clone the repository to your local machine and run
the `setupDevEnv.sh` bash script. This will replace the configuration files
with those in this repository and then source those that need to be source.
Then the environment will be all set up with just a few commands. Once the 
script has been run, it can be executed again and the most recently replaced
settings can be restored. However, only the most recent settings can be 
restored. 

**Note:** Executable privileges will need to be added to the script for it 
to be run: `chmod +x setupDevEnv.sh`. Also, for the terminal to immediately 
reflect the .bashrc changes, run the sript like this: `. ./setupDevEnv.sh`

Enjoy!

## Current Setup Configuration

### .bashrc
* Colored Terminal
* Bash Aliases

### .vimrc
* Map `jk` to `Esc`

### .gitignore_global
* Ignore `.vscode/`
* Runs `git config --global core.excludesfile ~/.gitignore_global`

## Additions

As additional environmental conveniences come up, this should be expanded
and maintained. This will make setting up a new environment easy and 
repeatable. 

## Configuring Vim

The `setupVim.sh` script will set everything up for you.
Simply run `./setupVim.sh` and follow any prompts.
Elevated privileges are required since additional packages are installed.

This script will copy the .vimrc file to ~/.vimrc, install any dependencies,
and install the plugins listed in the .vimrc.
See the script for details.

Before doing the following, make sure the `.vimrc` file of this repo is copied
to ~/.vimrc first.

Install `vim-plug` to manage plugins more easily:

```bash
curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

Start Vim, and run the following to install the plugins defined in the .vimrc file:

You can now start vim, and everything should be set up.

To set up a project with YouCompleteMe

- To find the function signatures and so forth, you need to
  Generate a compilation database. This can be done when running cmake by 
  adding the required flag to the rest of them:
  `-DCMAKE_EXPORT_COMPILE_COMMANDS=ON`.
- Then symlink the generated `compile_commands.json` file to the root of the
  project: `ln -sf ~/full/path/to/compile_commands.json ~/full/path/to/project/root`
- Now when you open a file within the project, things should work
- Here's an example of a compile command that can be run from anywhere to compile
  a cmake C++ project:
  `(cd ~/path/to/build_dir/; cmake . -DCMAKE_EXPORT_COMPILE_COMMANDS=ON -DDEBIAN_BUILD=True -DCMAKE_BUILD_TYPE=Debug; make -j $(nproc);)`

### Customized Vim Usage Tips

Here are some commonly used key commands when using vim with the .vimrc in this repo.

| Command  | Action |
|----------|--------|
| i        | Enter insert mode |
| jk       | Exit insert mode or other commands (Esc equivalent) |
| j        | Move the cursor down when not in insert mode |
| k        | Move the cursor up when not in insert mode |
| h        | Move the cursor left when not in insert mode |
| l        | Move the cursor right when not in insert mode |
| Shift+:  | Enters the command mode at the bottom |
| :w       | Write/save the buffer |
| :q       | Quit and close the buffer |
| :qa      | Quit and close all buffers |
| :q!      | Quit and close without saving |
| y        | Yank/Copy selection |
| yy       | Yank/Copy the whole line |
| p        | Paste |
| dd       | Delete a whole line |
| u        | Undo |
| Ctrl+r   | Redo |
| r        | Replace the character under the cursor |
| cw       | Change the word under the cursor |
| w        | Move the cursor forward a word |
| b        | Move the cursor back a word |
| v        | Visual mode - allows you to select text for copying or whatever |
| /        | Enter search mode - just type what you're looking for after pushing this key and then hit enter |
| *        | Search all occurances of what's under the cursor |
| n        | Move to the next search occurance |
| N        | Move to the previous search occurance |
| Ctrl+l   | Clear the highlights |
| ,t       | Toggle opening the NERDTree window for directory navigation |
| ff       | This will focus the cursor in the NERDTree window - helpful after opening a tab or something |
| ,f       | This will open the NERDTree window with the cursor on the file currently in the editor |
| t        | If you hit this key in the NERDTree window, a new tab will be opened and switched to for the selected file |
| T        | If you hit this key in the NERDTree window, a new tab will be opened but not switched to for the selected file |
| J        | Switch to the tab to the left |
| K        | Switch to the tab to the right |
| ,jd      | GoTo the declaration or definition of whatever is under the cursor (YouCompleteMe) |
| Ctrl+o   | Go back to wherever you jumped from |
| %s/searchText/replaceText/gc | Search and replace globally in the file and ask for a confirmation for each replacement |
| :vsp     | Split the window vertically |
| :sp      | Split the window horizontally |
| Ctrl+ww  | Switch to another window |
| Ctl+v    | Enter visual block mode |
| I        | When in visual block mode, this will put the characters typed on every selected line after pressing 'jk' or Esc | 
| 0        | Go to the first of the line |
| $        | Go to the end of the line |
| <line#>gg| Go to the line number
| gg       | Go to the top of the buffer |
| GG       | Go to the bottom of the buffer |
|:colorscheme \<name\> | Change the colorscheme |
| q\<character\> | Begin recording a macro (series of key commands), escape, press 'q' to stop recording |
| @\<character\> | Execute the commands recorded in the macro identified by \<character\> |
| #@\<character\> | Execute the macro # of times |
| :term | Open a terminal in another window below the current one |
| :vert term | Open a terminal in another window to the side of the current one |
| Ctrl+w N | Enter vim text mode inside of an open terminal window (hit 'i' to exit) |
| m\<character\> | Set a marker named <character> at cursor location |
| \`\<character\> | Go to marker indicated by <character> |
