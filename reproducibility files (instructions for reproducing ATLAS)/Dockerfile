# Step 1: Use Ubuntu as the base image
FROM ubuntu:20.04

# Step 2: Set up the working directory inside the container
WORKDIR /app

# Step 3: Install dependencies (Miniconda and other required tools)
RUN apt-get update && apt-get install -y \
    wget bzip2 && \
    wget -O miniconda.sh https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
    bash miniconda.sh -b -p /opt/conda && \
    rm miniconda.sh && \
    /opt/conda/bin/conda init

# Step 4: Add Conda to the system PATH
ENV PATH="/opt/conda/bin:$PATH"

# Step 5: Copy your project files into the container
COPY . /app

# Step 6: Create the Conda environment from environment.yml
RUN conda env create -f environment.yml

# Step 7: Activate the Conda environment
RUN echo "source activate atlas_env" > ~/.bashrc
ENV CONDA_DEFAULT_ENV atlas_env
ENV PATH /opt/conda/envs/atlas_env/bin:$PATH

# Step 8: Default command to keep the container running (change as needed)
CMD ["bash"]
