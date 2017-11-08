FROM fedora:latest
MAINTAINER a4neg@yandex.ru

ENV LC_ALL=C.UTF-8 LANG=ru_RU.UTF-8 LANGUAGE=ru_RU.UTF-8 TERM=xterm
RUN dnf -y groupinstall 'Xfce Desktop' && \
    dnf -y install \
    supervisor \
    xrdp \
    && dnf clean all

RUN useradd foo && \
    echo foo:bar | chpasswd
    echo datch:123 | chpasswd
    echo admin:123456 | chpasswd

# http://sigkillit.com/2013/02/26/how-to-remotely-access-linux-from-windows/
COPY etc/ /etc/

# Allow all users to connect via RDP.
RUN sed -i '/TerminalServerUsers/d' /etc/xrdp/sesman.ini && \
    sed -i '/TerminalServerAdmins/d' /etc/xrdp/sesman.ini

EXPOSE 3389
CMD ["supervisord", "-n"]

ARG CI_BUILD_URL
ARG BUILD_DATE
ARG VCS_REF

LABEL \
    io.github.jumanjiman.ci-build-url=${CI_BUILD_URL} \
    io.github.jumanjiman.build-date=${BUILD_DATE} \
    io.github.jumanjiman.vcs-ref=${VCS_REF} \
    io.github.jumanjiman.version="Fedora" \
    io.github.jumanjiman.license="GPL v3" \
    io.github.jumanjiman.docker.dockerfile="/fedora/Dockerfile" \
    io.github.jumanjiman.vcs-type="Git" \
    io.github.jumanjiman.vcs-url="https://github.com/a4neg/docker-xrdp.git"
