FROM rockylinux:9
ARG USERNAME=carlos
ARG USER_UID=1000   

RUN dnf update -y \
    && dnf group install "Development Tools" -y \
    && dnf install -y openssh sudo \
                      bash-completion vim tmux git \
    && dnf clean all \
    && useradd --uid $USER_UID $USERNAME \
    && usermod -aG wheel $USERNAME \
    && echo 'dont-do-this-in-prod' | passwd --stdin $USERNAME

USER $USERNAME
EXPOSE 22 80 1313 3000 5000 8000 8080 9000
WORKDIR /home/$USERNAME
CMD ["tail", "-f", "/dev/null"]
# CMD ["/bin/bash"]