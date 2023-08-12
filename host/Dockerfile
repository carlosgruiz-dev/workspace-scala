FROM rockylinux:9
ARG USERNAME=carlos
ARG USER_UID=1000   

RUN dnf update -y 
RUN dnf install -y openssh sudo bash-completion vim tmux git
RUN dnf clean all
RUN useradd --uid $USER_UID $USERNAME 
RUN usermod -aG wheel $USERNAME 
RUN echo 'dont-do-this-in-prod' | passwd --stdin $USERNAME
WORKDIR /home/$USERNAME
USER $USERNAME
RUN curl -fL "https://github.com/coursier/launchers/raw/master/cs-x86_64-pc-linux.gz" | gzip -d > cs
RUN chmod +x cs
RUN ./cs setup --jvm 15 -y
RUN rm cs
RUN echo 'eval "$(cs java --jvm 15 --env)"' >> /home/$USERNAME/.profile
RUN echo ". ~/.profile" >> /home/$USERNAME/.bashrc

EXPOSE 22 80 1313 3000 5000 8000 8080 9000

CMD ["tail", "-f", "/dev/null"]
# CMD ["/bin/bash"]
