# Cell-based modelling with Chaste

In this session, you'll work through a notebook that builds and runs a simple cell-based simulation, following on from the morning's talks. This is a hands-on introduction to [PyChaste](https://chaste.github.io/pychaste/), the Python interface to Chaste.

There are multiple ways to get set up for this session, described below. We recommend using the codespaces option, but you can try different options and pick whichever works best for you.

## Codespace instructions

> [!TIP]
> This is the recommended option. No local install is required, and you get access to a virtual machine with lots of CPU cores and memory.

> [!IMPORTANT]
> You'll need a GitHub account to use Codespaces. If you don't have one, [sign up](https://github.com/signup) and continue with the following instructions.

1. Go to the [Chaste repository](https://github.com/Chaste/Chaste) and switch to the `workshop-2026` branch.
2. Click **Code > Codespaces > "..." > New with options...**
3. Under **Dev container configuration**, choose the PyChaste configuration (`chaste/pychaste` image).
4. Choose a machine type — 4 cores / 16 GB RAM is recommended if available.
5. Click **Create codespace** and wait for it to build.
6. Once the codespace is ready, create a `notebooks` folder in the root of the source tree.
7. Open the [workshop notebook](https://colab.research.google.com/drive/1zgoqilNJAMf0frdSzJ71yERnDPyaNnWY) in Colab, then use **File > Download > Download .ipynb** to save it locally.
8. Drag the downloaded `.ipynb` file into the `notebooks` folder in the codespace's file explorer, then open it and select the PyChaste kernel.

## Local conda instructions

> [!NOTE]
> Local conda installation is supported on Linux and macOS only. On Windows, run these steps from within [WSL](https://learn.microsoft.com/windows/wsl/install).

If you'd rather work on your own laptop:

1. Install [Miniconda](https://www.anaconda.com/docs/getting-started/miniconda/install) or [Anaconda](https://www.anaconda.com/docs/getting-started/anaconda/install) if you don't already have it.
2. Install [`mamba`](https://mamba.readthedocs.io) into your base environment as dependency resolution with plain `conda` can be very slow:
   ```
   conda install -n base -c conda-forge mamba
   ```
3. Create a conda environment for PyChaste:
   ```
   mamba create -n pychaste -c pychaste -c conda-forge chaste
   conda activate pychaste
   ```
4. Install Jupyter Lab into the environment and launch it:
   ```
   mamba install -c conda-forge jupyterlab
   jupyter lab
   ```
   If you already have Jupyter Lab installed system-wide, you don't need it in the `pychaste` environment. Instead, install `ipykernel` and register the environment as a kernel instead:
   ```
   mamba install -c conda-forge ipykernel
   python -m ipykernel install --user --name pychaste --display-name "Python (pychaste)"
   ```
   Then launch your system-wide `jupyter lab` and select the "Python (pychaste)" kernel when you open the notebook.
5. Open the [workshop notebook](https://colab.research.google.com/drive/1zgoqilNJAMf0frdSzJ71yERnDPyaNnWY) in Colab, use **File > Download > Download .ipynb** to save it locally, then import it into Jupyter Lab (**File > Open**) and open it.

## Local docker instructions

> [!NOTE]
> This option works on Linux, macOS and Windows, but you'll need [Docker](https://docs.docker.com/get-started/get-docker/) installed and running.

1. Install [Docker](https://docs.docker.com/get-started/get-docker/) if you don't already have it, and make sure it is running.
2. Pull the PyChaste image (this is a few GB, so allow some time):
   ```
   docker pull chaste/pychaste
   ```
3. Start a container, exposing the JupyterLab server on port 8888:
   ```
   docker run -it --init --rm -p 8888:8888 chaste/pychaste
   ```
4. Open `http://localhost:8888` in your browser. If you are prompted for a token, copy it from the terminal output where you launched the container.
5. Open the [workshop notebook](https://colab.research.google.com/drive/1zgoqilNJAMf0frdSzJ71yERnDPyaNnWY) in Colab, use **File > Download > Download .ipynb** to save it locally, then drag it into the JupyterLab environment, or use the **Upload** button in the JupyterLab file browser.
6. Open the uploaded notebook and run it.

> [!TIP]
> The container is started with `--rm`, so anything saved inside it is lost when it stops. Download any results you want to keep from the JupyterLab file browser before exiting.

## Local devcontainer instructions

This gives you the same setup as the Codespaces option, but running locally through VS Code and Docker instead of in the cloud.

> [!TIP]
> On Windows, run these steps from within [WSL](https://learn.microsoft.com/windows/wsl/install).

> [!NOTE]
> You'll need [git](https://git-scm.com/downloads), [Docker](https://docs.docker.com/get-started/get-docker/), [VS Code](https://code.visualstudio.com/download) and the [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) installed.

1. Clone the Chaste repository and switch to the `workshop-2026` branch:
   ```
   git clone https://github.com/Chaste/Chaste.git
   cd Chaste
   git checkout workshop-2026
   ```
2. Open the folder in VS Code:
   ```
   code .
   ```
3. If prompted, click **Reopen in Container**. Otherwise, run **Dev Containers: Reopen in Container** from the Command Palette, and choose the PyChaste configuration. VS Code will pull the image and start the container — this might take a while the first time.
4. Once the container is ready, create a `notebooks` folder in the root of the source tree.
5. Open the [workshop notebook](https://colab.research.google.com/drive/1zgoqilNJAMf0frdSzJ71yERnDPyaNnWY) in Colab, use **File > Download > Download .ipynb** to save it locally, then drag it into the `notebooks` folder in the VS Code file explorer.
6. Open the notebook and select the PyChaste kernel.

## Colab instructions

> [!NOTE]
> Using Colab with conda packages can be unstable, so use it only if the other options aren't working for you. Colab is provided here as a fallback.

[Open the notebook in Colab](https://colab.research.google.com/drive/1zgoqilNJAMf0frdSzJ71yERnDPyaNnWY) and follow the instructions at the top on Colab prep.


## Next Steps

Once you've completed the notebook, take a look at the rest of the [PyChaste tutorials](https://chaste.github.io/pychaste/tutorials/).
