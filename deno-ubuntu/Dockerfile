FROM ubuntu:focal

RUN groupadd --gid 1000 gdeno \
  && useradd --uid 1000 --gid gdeno --shell /bin/bash --create-home udeno

ENV DENO_VERSION=1.0.1

RUN apt-get -qq update \
 && apt-get upgrade -y -o Dpkg::Options::="--force-confold" \
 && apt-get -qq install -y ca-certificates curl unzip --no-install-recommends \
 && curl -fsSL https://github.com/denoland/deno/releases/download/v${DENO_VERSION}/deno-x86_64-unknown-linux-gnu.zip \
         --output deno.zip \
 && unzip deno.zip \
 && rm deno.zip \
 && chmod 777 deno \
 && mv deno /usr/bin/deno \
 && apt-get -qq remove -y ca-certificates curl unzip \
 && apt-get -y -qq autoremove \
 && apt-get -qq clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp

USER udeno

WORKDIR /home/udeno/app

# ENTRYPOINT ["deno"]
# CMD ["run", "https://deno.land/std/examples/welcome.ts"]