---
title: "Local AI Server"
---

# Setting Up a Local AI Server with Ollama and OpenUI

Artificial intelligence is revolutionizing industries, and setting up a local AI server is an empowering step to take control of AI capabilities for personal or professional projects. This blog will walk you through how I successfully set up a local AI server using **Ollama** and **OpenUI**, managed Python environments with **pyenv**, and tackled challenges along the way.

## Why Set Up a Local AI Server?

Having a local AI server allows for:
- Full control over model usage and configuration.
- Enhanced privacy by processing data locally.
- The ability to experiment with cutting-edge AI models without relying on cloud services.

For this project, I chose to deploy the **Llama 3** model, a powerful language model, and used OpenUI for a user-friendly interface.

---

## Prerequisites

Before we dive in, ensure your system meets the following requirements:

- **Operating System:** Ubuntu 22.04 (or compatible Linux distribution).
- **Graphics:** A capable GPU is ideal, though I worked with Intel® Iris® Xe Graphics.
- **Tools:** Docker, pyenv, and Ollama CLI installed.

### Key Technologies Used
- **Ollama:** To manage and run AI models locally.
- **OpenUI:** A simple interface to interact with the AI models.
- **pyenv:** To manage multiple Python versions effortlessly.

---

## Step 1: Installing Ollama

Ollama is a CLI-based tool to download and run AI models. Follow these steps to install it:

1. Download and install Ollama by running:
   ```bash
   curl -sSL https://ollama.ai/install.sh | sh
   ```
2. Verify the installation:
   ```bash
   ollama version
   ```

3. Pull the Llama 3 model:
   ```bash
   ollama pull llama3
   ```

*Note: If you encounter a DNS or network issue, check your internet connection or DNS settings.*

---

## Step 2: Setting Up Docker and Running OpenUI

Docker is essential for running OpenUI containers to interact with AI models:

1. Install Docker:
   ```bash
   sudo apt update
   sudo apt install docker.io
   ```

2. Add your user to the Docker group to avoid using `sudo` for every command:
   ```bash
   sudo usermod -aG docker $USER
   ```
   Log out and log back in to apply the changes.

3. Run the OpenUI container:
   ```bash
   sudo docker run -d --network=host -v open-webui:/app/backend/data -e OLLAMA_BASE_URL=http://127.0.0.1:11434 --name open-webui --restart always ghcr.io/open-webui/open-webui:main
   ```

If you encounter an error about container name conflicts, remove the existing container:
   ```bash
   sudo docker rm open-webui
   ```
   Then rerun the above command.

---

## Step 3: Managing Python Versions with pyenv

To manage Python versions for additional tools and scripts:

1. Install pyenv:
   ```bash
   curl https://pyenv.run | bash
   ```

2. Add pyenv to your shell profile:
   ```bash
   echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
   echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
   echo 'eval "$(pyenv init --path)"' >> ~/.bashrc
   ```
   Then reload your shell:
   ```bash
   source ~/.bashrc
   ```

3. Install a specific Python version:
   ```bash
   pyenv install 3.10
   pyenv global 3.10
   ```
   *Note: If you encounter a `no acceptable C compiler found` error, install build dependencies:
   ```bash
   sudo apt install build-essential
   ```
   and retry.*

---

## Step 4: Interacting with the AI Model

1. Start the OpenUI interface:
   Open your web browser and navigate to `http://localhost:11434`. You should see a user interface to interact with Llama 3.

2. Test the model by entering prompts and observing responses.

---
![](https://github.com/V0ldii/annu/blob/main/static/images/ai1.jpeg?raw=true)

## Challenges Faced and Solutions

- **Network Issues:** DNS misconfigurations were resolved by switching to Google DNS (8.8.8.8).
- **Docker Permissions:** Adding my user to the Docker group eliminated the need for `sudo`.
- **Python Build Errors:** Installing `build-essential` resolved missing GCC errors during Python installation.

---

## Final Thoughts

This project was both challenging and rewarding. Setting up a local AI server with Ollama and OpenUI offers independence, privacy, and a hands-on experience with advanced AI models. The journey taught me the importance of debugging, system configuration, and persistence.

Feel free to clone my repository and try it yourself: [GitHub Repository Link]

If you have any questions or insights, let’s discuss in the comments!

