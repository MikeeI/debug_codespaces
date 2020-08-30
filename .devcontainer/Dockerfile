ARG VARIANT=14
FROM mcr.microsoft.com/vscode/devcontainers/javascript-node:${VARIANT}

ARG INCLUDE_WORKER_TEMPLATE=https://github.com/cloudflare/worker-template
ENV USER=node

COPY ./npm/* /home/node/

USER node
WORKDIR /home/node/wrangler

RUN cd /home/node && \
    npm install --cache=/home/node/.cache && \
    mkdir -p /home/node/wrangler && \
    if [[ ! -z $INCLUDE_WORKER_TEMPLATE ]]; then cd /home/node && /home/node/.wrangler/out/wrangler generate worker "${INCLUDE_WORKER_TEMPLATE}" && cd "/home/node/worker" && npm install --cache=/home/node/.cache && cd /home/node/worker && /home/node/.wrangler/out/wrangler build; fi


ENTRYPOINT ["/home/node/.wrangler/out/wrangler"]

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

# [Optional] Uncomment if you want to install an additional version of node using nvm
# ARG EXTRA_NODE_VERSION=10
# RUN su node -c "source /usr/local/share/nvm/nvm.sh && nvm install ${EXTRA_NODE_VERSION}"

# [Optional] Uncomment if you want to install more global node modules
# RUN sudo -u node npm install -g <your-package-list-here>
