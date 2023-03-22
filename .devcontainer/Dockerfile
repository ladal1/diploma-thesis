# Source: https://gitlab.fit.cvut.cz/KAM/docker-texlive/-/blob/028ac9aeb6ad4e20bdb28d117cbac69277799d98/Dockerfile

FROM ruby:3.1.3-slim-bullseye

RUN apt-get update -qq && apt-get install -y \
    wget unzip xz-utils ed \
    libswitch-perl \
    gnupg

COPY ./texlive.profile /tmp/

RUN cd /tmp && wget -qO- https://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz | tar xz \
    && /tmp/install-tl*/install-tl -profile /tmp/texlive.profile \
    && tlmgr init-usertree \
    && tlmgr install latexmk pgf memoir setspace caption titlesec mathtools ellipsis pdfpages lipsum csquotes listings pdflscape minted fontspec todonotes pgfplots polyglossia booktabs enumitem multirow blindtext cleveref standalone beamer subfig textcase \
    && luaotfload-tool latexindent -u \
    && rm -rf /tmp/install-tl-*

# RUN cpan -i YAML::Tiny \
#     && cpan -i File::HomeDir

RUN apt-get install -y --no-install-recommends python3 python3-pip libfontconfig make git && \
    apt-get clean && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/ /tmp/* /var/tmp/* && \
    pip3 install pygments && ln -f /usr/bin/python3.9 /usr/bin/python

WORKDIR /tmp/workdir

# Uncomment if running on M1/M2 Mac and comment out the ENV PATH line below
# ENV PATH="/usr/local/texlive/bin/aarch64-linux:${PATH}"
ENV PATH="/usr/local/texlive/bin/x86_64-linux:${PATH}"
ENV TERM='xterm-256color'
