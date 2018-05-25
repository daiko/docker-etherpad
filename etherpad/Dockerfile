FROM node:latest

RUN apt-get update \
    && apt-get install -y gzip git curl python libssl-dev pkg-config build-essential abiword tidy \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN npm i npm@latest -g

RUN git clone https://github.com/ether/etherpad-lite.git /opt/etherpad
RUN npm install --prefix /opt/etherpad ep_padlist
RUN sed -i "s#/<%= pad.toString() %>#/p/<%= pad.toString() %>#g" /opt/etherpad/node_modules/ep_padlist/templates/pads.html
RUN npm install --prefix /opt/etherpad ep_adminpads
RUN npm install --prefix /opt/etherpad ep_comments_page

RUN useradd -mUs /bin/bash etherpad
RUN chown -R etherpad:etherpad /opt/etherpad


WORKDIR /opt/etherpad
USER etherpad:etherpad

ENTRYPOINT ["/opt/etherpad/bin/run.sh"]
