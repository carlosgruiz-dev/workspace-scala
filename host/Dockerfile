FROM rockylinux:9
ARG USERNAME=carlos
ARG USER_UID=1000   

# Update and Installs Linux packages
RUN dnf update -y
RUN dnf group install "Development Tools" -y && dnf install -y openssh sudo bash-completion vim tmux git
RUN dnf clean all
RUN useradd --uid $USER_UID $USERNAME && usermod -aG wheel $USERNAME 
RUN echo 'dont-do-this-in-prod' | passwd --stdin $USERNAME
WORKDIR /home/$USERNAME
USER $USERNAME

# Installs coursier (Scala)
RUN curl -fL "https://github.com/coursier/launchers/raw/master/cs-x86_64-pc-linux.gz" | gzip -d > cs
RUN chmod +x cs && ./cs setup --jvm 15 -y && rm cs
RUN mkdir /home/$USERNAME/.bashrc.d/
RUN cp /home/$USERNAME/.profile /home/$USERNAME/.bashrc.d/scala-tools
RUN echo 'eval "$(cs java --jvm 15 --env)"' >> /home/$USERNAME/.bashrc.d/scala-tools

# Installs nvm (JavaScript)
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.4/install.sh | bash
RUN . "/home/$USERNAME/.nvm/nvm.sh" && nvm install --lts=hydrogen \
    && npm install -g http-server yarn

EXPOSE 22 80 1313 3000 5000 8000 8080 9000

CMD ["tail", "-f", "/dev/null"]
