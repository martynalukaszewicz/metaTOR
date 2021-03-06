Bootstrap: docker
From: ubuntu:18.04

%labels
  Maintainer tpall

%post
  # Get dependencies
  apt-get update
  apt-get install -y --no-install-recommends \
  git \
  python \
  python-pip \
  python3-setuptools \
  python3 \
  python3-dev \
  python3-pip \
  python3-virtualenv \
  bowtie2 \
  samtools \
  hmmer \
  prodigal \
  libfreetype6-dev \
  libpng-dev \
  pkg-config \
  wget \
  pigz
  
  mkdir -p /tools
  cd /tools
  
  # Fetching louvain
  mkdir -p /tools/louvain
  wget -q https://lip6.github.io/Louvain-BinaryBuild/louvain_linux.tar.gz -O /tools/louvain/louvain.tar.gz
  cd /tools/louvain
  tar -xzf louvain.tar.gz
  chmod +x /tools/louvain/*
  rm -f /tools/louvain/louvain.tar.gz
  
  # Fetching HMMs
  mkdir -p /HMM_databases
  cd /HMM_databases
  wget -q http://dl.pasteur.fr/fop/LItxiFe9/hmm_databases.tgz
  tar -xzf /HMM_databases/hmm_databases.tgz
  rm -f /HMM_databases/hmm_databases.tar.gz
  cd /
  
  # Add tools to path during runtime
  echo 'export PATH=$PATH:/tools:/tools/louvain:/HMM_databases' >>$SINGULARITY_ENVIRONMENT
  
  # Install metator and requests
  pip3 install requests
  pip3 install git+https://github.com/koszullab/metator.git
  chmod 777 -R /usr/local/lib/python3.6/dist-packages/metator/bin/

  # Clean up
  rm -rf /var/lib/apt/lists/*

%runscript
  exec metator "$@"
