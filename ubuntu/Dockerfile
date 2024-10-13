# Use Ubuntu 24.04 as the base image
FROM ubuntu:24.04

# Set environment variables to prevent interactive prompts and ensure Conda is in PATH
ENV DEBIAN_FRONTEND=noninteractive
ENV PATH="/opt/conda/bin:$PATH"

# Update system and install necessary tools
RUN apt update && apt install -y \
    wget \
    bzip2 \
    curl \
    git \
    && rm -rf /var/lib/apt/lists/*

# Install Miniconda
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O /tmp/miniconda.sh && \
    bash /tmp/miniconda.sh -b -p /opt/conda && \
    rm /tmp/miniconda.sh

# Initialize Conda for bash shells
RUN /opt/conda/bin/conda init bash

# Create and activate the llm environment
RUN /opt/conda/bin/conda create -n llm python=3.10 && \
    echo "conda activate llm" >> ~/.bashrc

# Set the working directory
WORKDIR /home/julius/llm

# Switch to non-root user (optional)
RUN useradd -m -u 5678 julius && chown -R julius /home/julius
USER julius

# Expose port 8080 for web services
EXPOSE 8080

# Ensure the Conda environment is activated by default
SHELL ["/bin/bash", "--login", "-c"]

# Run Python version check or replace with your app entrypoint
CMD ["python", "--version"]
