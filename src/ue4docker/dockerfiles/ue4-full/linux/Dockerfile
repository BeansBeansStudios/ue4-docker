ARG NAMESPACE
ARG TAG
ARG PREREQS_TAG
FROM ${NAMESPACE}/ue4-minimal:${TAG}-${PREREQS_TAG}

# Install ue4cli
ARG UE4CLI_VERSION="ue4cli>=0.0.45"
USER root
RUN pip3 install --upgrade pip setuptools wheel
RUN pip3 install "${UE4CLI_VERSION}"
RUN chown -R ue4:ue4 /tmp/project


# Explicitly set the configuration directory for ue4cli
# (This prevents things from breaking when using CI/CD systems that override the $HOME environment variable)
USER ue4
ENV UE4CLI_CONFIG_DIR /home/ue4/.config/ue4cli
RUN ue4 setroot /home/ue4/UnrealEngine

# Install Perforce
RUN curl -fsSL https://package.perforce.com/perforce.pubkey | sudo gpg --dearmor -o /usr/share/keyrings/perforce.gpg
RUN echo 'deb [signed-by=/usr/share/keyrings/perforce.gpg] https://package.perforce.com/apt/ubuntu   jammy release' | sudo tee /etc/apt/sources.list.d/perforce.list
RUN sudo apt-get update && sudo apt-get install -y --no-install-recommends helix-cli=2023.2-2535420~jammy
