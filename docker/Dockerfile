FROM debian
ARG LOGIN
ARG PASSWORD
ARG PROXY
ARG PORT
ARG DOMAINE
RUN apt-get update && apt-get install -y curl gnupg git npm
RUN curl -sL https://deb.nodesource.com/setup_9.x | bash -
RUN apt-get update && apt-get install -y nodejs
RUN rm -rf /var/lib/apt/lists/*
WORKDIR /opt/meeteasier
RUN git clone https://github.com/danxfisher/MeetEasier.git /opt/meeteasier
COPY flightboard.config.js /opt/meeteasier/ui-react/src/config/flightboard.config.js
COPY singleRoom.config.js /opt/meeteasier/ui-react/src/config/singleRoom.config.js
RUN sed -i 's/SVCACCT_EMAIL\@DOMAIN\.COM/'"$LOGIN"'/g' config/auth.js && sed -i 's/PASSWORD/'"$PASSWORD"'/g' config/auth.js && sed -i 's/DOMAIN\.COM/'"$DOMAINE"'/g' config/auth.js \
  && sed -i 's/localhost/'"$PROXY"'/g' ui-react/package.json   && sed -i 's/8080/'"$PORT"'/g' ui-react/package.json
RUN npm install
RUN cd ui-react && npm install && npm run build
CMD ["node","server.js"]
