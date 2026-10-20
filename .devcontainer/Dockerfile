FROM rubylang/ruby:3.2.10-dev-jammy

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=1000

RUN apt-get update \
  && apt-get install -y --no-install-recommends libyaml-dev sudo \
  && groupadd --gid ${USER_GID} ${USERNAME} \
  && useradd --uid ${USER_UID} --gid ${USER_GID} -m -s /bin/bash ${USERNAME} \
  && usermod --append --groups sudo ${USERNAME} \
  && echo "${USERNAME} ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/${USERNAME} \
  && chmod 0440 /etc/sudoers.d/${USERNAME} \
  && mkdir -p /home/${USERNAME}/.bundle \
  && chown -R ${USERNAME}:${USERNAME} /home/${USERNAME} \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

ENV BUNDLE_PATH=/home/${USERNAME}/.bundle
ENV GEM_HOME=${BUNDLE_PATH}/ruby/3.2.0
ENV GEM_PATH=${GEM_HOME}
ENV PATH=${GEM_HOME}/bin:${PATH}

COPY codespaces-prompt.sh /etc/profile.d/codespaces-prompt.sh

RUN chmod 0644 /etc/profile.d/codespaces-prompt.sh \
  && echo 'source /etc/profile.d/codespaces-prompt.sh' >> /home/${USERNAME}/.bashrc

USER ${USERNAME}
