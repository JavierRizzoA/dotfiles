#-------------------------------------------------------------------------------
# "THE BEER-WARE LICENSE" (Revision 42):
# Javier Rizzo <javierrizzoa@gmail.com> wrote this file. As long as you retain
# this notice you can do whatever you want with this stuff. If we meet some day,
# and you think this stuff is worth it, you can buy me a beer in return.
#-------------------------------------------------------------------------------

VIMPACKAGES=false
DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" && pwd )"

echo $DIR

#true: VIM; false: NVIM
function install-vim-packages {
  mkdir -p vim/bundl    e
  git clone https://github.com/VundleVim/Vundle.vim.git "$DIR/vim/bundle/Vundle.vim"
  if $1 ;
  then
    vim +PluginInstall +qall ;
  else
    nvim +PluginInstall +qall ;
  fi
}

read -p "Install BASH files? " -n 1 -r
echo
if [[ ! $REPLY =~ ^[Nn]$ ]]
then
  cd ~
  rm -r .bashrc
  ln -s "$DIR/bash/bashrc" .bashrc
fi

read -p "Install VIM files? " -n 1 -r
echo
if [[ ! $REPLY =~ ^[Nn]$ ]]
then
  install-vim-packages true
  VIMPACKAGES=true
  cd ~
  mkdir -p .vim
  cd .vim
  rm -f vimrc
  ln -s "$DIR/vim/vimrc" vimrc
  rm -rf bundle
  ln -s "$DIR/vim/bundle" bundle
fi

read -p "Install NEOVIM files?" -n 1 -r
echo
if [[ ! $REPLY =~ ^[Nn]$ ]]
then
  if ! $VIMPACKAGES ;
  then
    install-vim-packages false ;
  fi
  cd $XDG_CONFIG_HOME
  mkdir -p nvim
  cd nvim
  rm -f init.vim
  ln -s "$DIR/vim/vimrc" init.vim
  rm -rf bundle
  ln -s "$DIR/vim/bundle" bundle
fi
