FROM alpine:3.20

# Install bash, git, curl, openssh-client
RUN apk add --no-cache ca-certificates bash git curl openssh-client

WORKDIR /usr/local/bin

ENV KUBECTL_VERSION=1.30.4
ENV KUSTOMIZE_VERSION=5.4.3

# Install kubectl
RUN curl -sLO https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl && \
    chmod +x ./kubectl

# Install kustomize
RUN curl -sLO https://github.com/kubernetes-sigs/kustomize/releases/download/kustomize/v${KUSTOMIZE_VERSION}/kustomize_v${KUSTOMIZE_VERSION}_linux_amd64.tar.gz && \
    tar -xzf kustomize_v${KUSTOMIZE_VERSION}_linux_amd64.tar.gz && \
    rm kustomize_v${KUSTOMIZE_VERSION}_linux_amd64.tar.gz && \
    chmod +x ./kustomize

# Disable host key checking (NOTE: makes you susceptible to man-in-the-middle attacks)
# WARNING: use only in docker container, if you use it with shell you will overwrite your user's ssh config
RUN mkdir -p ~/.ssh && chmod 700 ~/.ssh && \
    echo -e "Host *\n\tStrictHostKeyChecking no\n\tUserKnownHostsFile /dev/null\n" > ~/.ssh/config
