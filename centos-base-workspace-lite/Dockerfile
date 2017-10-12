FROM zeroc0d3lab/centos-base-consul:latest
MAINTAINER ZeroC0D3 Team <zeroc0d3.team@gmail.com>

#-----------------------------------------------------------------------------
# Set Environment
#-----------------------------------------------------------------------------
ENV PATH_HOME=/home/docker \
    PATH_WORKSPACE=/home/docker/workspace

#-----------------------------------------------------------------------------
# Set Group & User for 'docker'
#-----------------------------------------------------------------------------
RUN mkdir -p ${PATH_HOME} \
    && groupadd docker \
    && useradd -r -g docker docker \
    && usermod -aG root docker \
    && chown -R docker:docker ${PATH_HOME} \
    && mkdir -p ${PATH_HOME}/git-shell-commands \
    && chmod 755 ${PATH_HOME}/git-shell-commands

#-----------------------------------------------------------------------------
# Find Fastest Repo & Update Repo
#-----------------------------------------------------------------------------
RUN yum makecache fast \
    && yum -y update

#-----------------------------------------------------------------------------
# Install Workspace Dependency (1)
#-----------------------------------------------------------------------------
RUN yum -y install \
           --setopt=tsflags=nodocs \
           --disableplugin=fastestmirror \
         git \
         git-core \
         zsh \
         gcc \
         gcc-c++ \
         autoconf \
         automake \
         make \
         libevent-devel \
         ncurses-devel \
         glibc-static \
         fontconfig \

#-----------------------------------------------------------------------------
# Install MySQL (MariaDB) Library
#-----------------------------------------------------------------------------
         mysql-devel \

#-----------------------------------------------------------------------------
# Install PostgreSQL Library
#-----------------------------------------------------------------------------
### PostgreSQL 9.2 (default)###
         postgresql-libs \
         postgresql-devel \

### PostgreSQL 9.6 ###
    && rpm -iUvh https://yum.postgresql.org/9.6/redhat/rhel-7-x86_64/pgdg-centos96-9.6-3.noarch.rpm \
    && yum install -y postgresql96-libs postgresql96-server postgresql96-devel \

#-----------------------------------------------------------------------------
# Install Workspace Dependency (2)
#-----------------------------------------------------------------------------
RUN yum -y install \
           --setopt=tsflags=nodocs \
           --disableplugin=fastestmirror \
         zlib \
         zlib-devel \
         patch \
         readline \
         readline-devel \
         libyaml-devel \
         libffi-devel \
         openssl-devel \
         bzip2 \
         bison \
         libtool \
         sqlite-devel

#-----------------------------------------------------------------------------
# Clean Up All Cache
#-----------------------------------------------------------------------------
RUN yum clean all

#-----------------------------------------------------------------------------
# Download & Install
# -) bash_it (bash + themes)
# -) oh-my-zsh (zsh + themes)
#-----------------------------------------------------------------------------
RUN rm -rf /root/.bash_it \
    && rm -rf /root/.oh-my-zsh \
    && touch /root/.bashrc \
    && touch /root/.zshrc \
    && cd /root \
    && git clone https://github.com/Bash-it/bash-it.git /root/bash_it \
    && git clone https://github.com/speedenator/agnoster-bash.git /root/bash_it/themes/agnoster-bash \
    && git clone https://github.com/robbyrussell/oh-my-zsh.git /root/oh-my-zsh \
    && mv /root/bash_it /root/.bash_it \
    && mv /root/oh-my-zsh /root/.oh-my-zsh

#-----------------------------------------------------------------------------
# Download & Install
# -) tmux + themes
#-----------------------------------------------------------------------------
RUN rm -rf /tmp/tmux \
    && rm -rf /root/.tmux/plugins/tpm \
    && touch /root/.tmux.conf \
    && git clone https://github.com/tmux-plugins/tpm.git /root/tmux/plugins/tpm \
    && git clone https://github.com/tmux/tmux.git /tmp/tmux \
    && git clone https://github.com/seebi/tmux-colors-solarized.git /root/tmux-colors-solarized \
    && mv /root/tmux /root/.tmux

RUN cd /tmp/tmux \
    && /bin/sh autogen.sh \
    && /bin/sh ./configure \
    && sudo make \
    && sudo make install

#-----------------------------------------------------------------------------
# Install Font Config
#-----------------------------------------------------------------------------
RUN mkdir -p /root/.fonts \
    && mkdir -p /root/.config/fontconfig/conf.d/ \
    && mkdir -p /usr/share/fonts/local \
    && wget https://github.com/powerline/powerline/raw/develop/font/PowerlineSymbols.otf -O /root/.fonts/PowerlineSymbols.otf \
    && wget https://github.com/powerline/powerline/raw/develop/font/10-powerline-symbols.conf -O /root/.config/fontconfig/conf.d/10-powerline-symbols.conf \
    && cp /root/.fonts/PowerlineSymbols.otf /usr/share/fonts/local/PowerlineSymbols.otf \
    && cp /root/.fonts/PowerlineSymbols.otf /usr/share/fonts/PowerlineSymbols.otf \
    && cp /root/.config/fontconfig/conf.d/10-powerline-symbols.conf /etc/fonts/conf.d/10-powerline-symbols.conf \
    && ./usr/bin/fc-cache -vf /root/.fonts/ \
    && ./usr/bin/fc-cache -vf /usr/share/fonts

#-----------------------------------------------------------------------------
# Download & Install
# -) dircolors (terminal colors)
#-----------------------------------------------------------------------------
RUN git clone https://github.com/Anthony25/gnome-terminal-colors-solarized.git /root/solarized \
    && mv /root/solarized /root/.solarized

#-----------------------------------------------------------------------------
# Setup TrueColors (Terminal)
#-----------------------------------------------------------------------------
COPY ./rootfs/root/colors/24-bit-color.sh /tmp/24-bit-color.sh
RUN chmod a+x /tmp/24-bit-color.sh; sync \
    && ./tmp/24-bit-color.sh

#-----------------------------------------------------------------------------
# Set PORT Docker Container
#-----------------------------------------------------------------------------
EXPOSE 22

#-----------------------------------------------------------------------------
# Set Volume Docker Workspace Lite
#-----------------------------------------------------------------------------
VOLUME [${PATH_HOME}, "/root"]

#-----------------------------------------------------------------------------
# Finalize (reconfigure)
#-----------------------------------------------------------------------------
COPY rootfs/ /

#-----------------------------------------------------------------------------
# Run Init Docker Container
#-----------------------------------------------------------------------------
ENTRYPOINT ["/init"]
CMD []