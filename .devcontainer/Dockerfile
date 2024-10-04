ARG BASE

FROM ${BASE} as base

ARG RAPIDS
ENV RAPIDS=${RAPIDS}

ARG CUDA
ENV CUDA_VERSION="${CUDA_VERSION:-${CUDA}}"

ENV PYTHON_PACKAGE_MANAGER="conda"

ARG SCCACHE_REGION="us-east-2"
ENV SCCACHE_REGION="$SCCACHE_REGION"
ARG SCCACHE_BUCKET="rapids-sccache-devs"
ENV SCCACHE_BUCKET="$SCCACHE_BUCKET"
ARG VAULT_HOST="https://vault.ops.k8s.rapids.ai"
ENV VAULT_HOST="$VAULT_HOST"

ENV HISTFILE="/home/coder/.cache/._bash_history"

RUN mkdir -p /home/coder/.{aws,cache,config/pip,local,out}

# ===== install common packages ==================================================================

RUN <<EOF

set -x

apt-get update;

# apt-get install -y --no-install-recommends  \
#     libboost-{regex,system,filesystem}-dev  \
#     ;

rm -rf /tmp/*;
rm -rf /var/tmp/*;
rm -rf /var/cache/apt/*;
rm -rf /var/lib/apt/lists/*;

EOF

FROM base as devel
FROM base as runtime