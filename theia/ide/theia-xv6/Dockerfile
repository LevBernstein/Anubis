# https://github.com/theia-ide/theia-apps/tree/master/theia-cpp-docker

FROM registry.digitalocean.com/anubis/theia-base:python-3.10 as theia

USER root
RUN set -ex; \
  apt-get update; \
  apt-get install -y --no-install-recommends \
    gdb git build-essential cmake \
    gcc-multilib g++-multilib libc6-dev \
    clangd \
    qemu-system-i386; \
  echo 'set auto-load safe-path /' > /etc/skel/.gdbinit; \
  echo 'source /opt/pwndbg/gdbinit.py' >> /etc/skel/.gdbinit; \
  git clone https://github.com/pwndbg/pwndbg.git /opt/pwndbg; \
  cd /opt/pwndbg; \
  ./setup.sh; \
  rm -rf /tmp/*; \
  rm -rf /usr/share/doc; \
  rm -rf /var/lib/apt/lists/*; \
  rm -rf /home/node/*; \
  find / -depth \
    \( -name .cache -o -name __pycache__ -o -name '*.pyc' -o -name .git -o -name .github \) \
    -exec 'rm' '-rf' '{}' '+';

USER anubis