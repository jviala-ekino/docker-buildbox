FROM alpine:3.4

ARG SONARSCANNER_VERSION

ENV PATH=/sonar-scanner/bin:/sonar-scanner/jre/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

ARG SONARSCANNER_VERSION
ARG CI_HELPER_VERSION

RUN echo "Starting ..." && \
    apk --update upgrade && apk add curl unzip make && \
    echo "Done base install!" && \
    
    echo "Starting Sonar Scanner" && \
    curl --insecure -o ./sonarscanner.zip -L https://sonarsource.bintray.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-${SONARSCANNER_VERSION}-linux.zip && \
    unzip sonarscanner.zip && \
    rm sonarscanner.zip && \
    mv sonar-scanner-${SONARSCANNER_VERSION}-linux sonar-scanner && \
    echo "Done Sonar Scanner!" && \

    echo "Install CI Helper" && \
    curl -sSL https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.23-r3/sgerrand.rsa.pub -o /etc/apk/keys/sgerrand.rsa.pub && \
    curl -sSL https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.23-r3/glibc-2.23-r3.apk -O && \
    apk add -q glibc-2.23-r3.apk && \
    rm /etc/apk/keys/sgerrand.rsa.pub glibc-2.23-r3.apk && \
    curl -sSL https://github.com/rande/gitlab-ci-helper/releases/download/${CI_HELPER_VERSION}/linux-amd64-gitlab-ci-helper -o /usr/bin/ci-helper && \
    chmod 755 /usr/bin/ci-helper && \
    echo "Done install CI Helper"  && \

    echo "Cleaning files!" && \
    rm -rf /tmp/* /var/cache/apk/* && \
    echo "Done!"
