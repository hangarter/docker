FROM sickcodes/docker-osx:latest

# Global dependencies
# Installs Homebrew
RUN gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
RUN curl -sSL https://get.rvm.io | bash -s stable --ruby \
  && source ~/.rvm/scripts/rvm \
  && rvm use 3.0.0 \
  && /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Installs dependencies (toolbox)
RUN eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)" \
  && brew install git \
  && brew install git-lfs \
  && brew install wget \
  && brew install htop \
  && git lfs install --system --skip-repo

# Disable default sound card, which removes ALSA warnings
ADD config/asound.conf /etc/

# Support forward compatibility for unity activation
RUN sudo chmod a+w /etc \
  && sudo chmod a+w /var/lib/dbus \
  && echo "576562626572264761624c65526f7578" > /etc/machine-id && mkdir -p /var/lib/dbus/ && ln -sf /etc/machine-id /var/lib/dbus/machine-id

# Used by Unity editor in "modules.json" and must not end with a slash.
ENV UNITY_PATH="/opt/unity"

# Fixes a Gradle crash while building for Android on Unity 2019 when there are accented characters in environment variables
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
