# Sets up a dev environment for FutureGPT
# This isn't really appropriate for public use for two reasons:
#   - We don't copy in FutureGPT2/src here; instead, it's
#     better to manually git clone the (private) repo after the docker build
#     so that it can be kept up to date
#   - Creates user and clones in personal dotfiles to make dev work more convenient (for me, wwu)

FROM runpod/pytorch:2.1.0-py3.10-cuda11.8.0-devel-ubuntu22.04

RUN apt-get update \
    && apt-get install -y vim rsync htop zsh

RUN useradd -ms /bin/zsh wwu
RUN usermod -aG sudo wwu
RUN chsh -s $(which zsh) wwu
USER wwu
WORKDIR /home/wwu

RUN pip install --upgrade pip \
    && pip install transformers datasets beir wandb lightning jupyterlab-vim
RUN git clone https://github.com/wiwu2390/dots_public.git $HOME/dots
RUN ln -s $HOME/dots/.vimrc $HOME/.vimrc
RUN curl -sSL https://raw.githubusercontent.com/alacritty/alacritty/master/extra/alacritty.info | tic -x -
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
RUN ln -s $HOME/dots/moonrise.zsh-theme $HOME/.oh-my-zsh/themes
# Need to do this after oh-my-zsh install, b/c it overwrites zsh
RUN rm $HOME/.zshrc
RUN ln -s $HOME/dots/.zshrc $HOME/.zshrc
RUN curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
RUN vim -c 'PlugInstall' -c 'qa!'

USER root

