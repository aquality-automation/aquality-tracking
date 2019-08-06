FROM alpine/git as clone
WORKDIR /app
ARG FRONTBRANCH
ENV FRONTBRANCH ${FRONTBRANCH:-master}
RUN git clone https://github.com/TrueAutomationValue/ReportingPortal---Frontend.git
RUN cd ReportingPortal---Frontend && git fetch origin && if [ ${FRONTBRANCH} != 'master' ]; then git checkout -t origin/${FRONTBRANCH}; fi

FROM node:10.15.3 as runTests
WORKDIR /app
COPY --from=clone /app/ReportingPortal---Frontend /app
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN echo 'deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main' | tee /etc/apt/sources.list.d/google-chrome.list
RUN apt-get update 
RUN apt-get -y install google-chrome-stable
RUN npm i
CMD npm run e2e:headless