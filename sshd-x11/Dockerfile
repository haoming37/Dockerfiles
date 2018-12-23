FROM ubuntu:16.04
# https://blog.n-z.jp/blog/2018-07-27-sshd-in-docker.html
RUN apt-get update && apt-get install -y --no-install-recommends \
    openssh-server \
    xauth \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
RUN mkdir /run/sshd
RUN echo 'root:password' | chpasswd
RUN sed -i 's/#\?PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
RUN echo AddressFamily inet >> /etc/ssh/sshd_config
#COPY authorized_keys /root/.ssh/authorized_keys
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]

#Install VisualStudioCode
RUN apt-get update && apt-get install -y --no-install-recommends \
    libasound2-dev \
    curl \
    libnotify4 \
    libnss3 \
    libxkbfile1 \
    libgconf-2-4 \
    libsecret-1-0 \
    libgtk-3-0 \
    libxss1 \
    libxtst-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
RUN curl -k -L -o vscode.deb https://go.microsoft.com/fwlink/?LinkID=760868 \
    && apt-get install -y ./vscode.deb \
    && rm vscode.deb
