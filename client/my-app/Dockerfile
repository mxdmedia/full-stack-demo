FROM node:10

ENV DEBIAN_FRONTEND=noninteractive

ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN apt-get update \
  && apt-get -y install --no-install-recommends apt-utils dialog 2>&1 \
  #
  # Verify git and needed tools are installed
  && apt-get -y install git iproute2 procps \
  && apt-get update \
  && apt-get -y install --no-install-recommends yarn \
  #
  # Install tslint, typescript, and angular cli globally
  && npm install -g tslint typescript \
  && npm install -g @angular/cli \
  #
  # Clean up
  && apt-get autoremove -y \
  && apt-get clean -y \
  && rm -rf /var/lib/apt/lists/*

# Switch back to dialog for any ad-hoc use of apt-get
ENV DEBIAN_FRONTEND=

COPY . /code
WORKDIR /code

RUN npm install
