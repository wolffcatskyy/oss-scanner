FROM debian:bookworm
RUN apt-get update && apt-get install -y --no-install-recommends shellcheck python3 python3-yaml git \
    && rm -rf /var/lib/apt/lists/*
COPY . /src
WORKDIR /src
RUN find . -name '*.sh' -not -path './.git/*' -print0 | xargs -0 -r -n1 bash -n
RUN shellcheck -S warning $(find . -name '*.sh' -not -path './.git/*') || echo "WARNING: shellcheck reported issues"
RUN python3 -c "import yaml; [yaml.safe_load(open(f)) for f in ['docker-compose.yml', 'sidecar-config.yaml']]; print('YAML OK')" || echo "WARNING: YAML validation failed"
