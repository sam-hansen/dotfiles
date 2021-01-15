FROM archlinux/base:latest
# Locales keyboard
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen \
 && locale-gen \
 && echo 'LANG="en_US.UTF-8"' > /etc/locale.conf
ENV LANG="en_US.UTF-8"
# Archlinux Deps
RUN pacman -Syu --noconfirm \ 
      sudo \
      binutils \
      util-linux \
      fakeroot \
      file \
      python \
      yajl \
      make \
      gcc \
      pkg-config \
      which \
      perl \
      automake \
      autoconf \
      gettext \
      patch \
      rsync \
      xorg-server-xephyr 
ENV PATH="${PATH}:/usr/bin/core_perl"
# Project deps
RUN pacman -S --noconfirm \ 
      ansible \
      jshon \
      git \
      neovim \
      mako \
      fish
# Fix tmp dir perms
RUN chmod 1777 /tmp
# Create test user
RUN useradd -m user \
 && chown -R user:user /home/user \
 && echo -e "user\nuser" | passwd user
RUN echo "user ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers 
# User run
USER user
WORKDIR /home/user/
ENV LANG="en_US.UTF-8"
COPY . .
CMD ["/bin/bash"]
