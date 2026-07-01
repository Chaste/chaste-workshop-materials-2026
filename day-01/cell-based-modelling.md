# Cell-based modelling with Chaste

In this session, you'll work through a notebook that builds and runs a simple cell-based simulation, following on from the morning's talks. This is a hands-on introduction to [PyChaste](https://chaste.github.io/pychaste/), the Python interface to Chaste.

There are three ways to get set up for this session, described below. Pick whichever suits you best.

## Codespace instructions

This is the recommended option. No local install is required.

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

## Local instructions

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
   If you already have Jupyter Lab installed system-wide, you don't need it in the `pychaste` environment — just install `ipykernel` and register the environment as a kernel instead:
   ```
   mamba install -c conda-forge ipykernel
   python -m ipykernel install --user --name pychaste --display-name "Python (pychaste)"
   ```
   Then launch your system-wide `jupyter lab` and select the "Python (pychaste)" kernel when you open the notebook.
5. Open the [workshop notebook](https://colab.research.google.com/drive/1zgoqilNJAMf0frdSzJ71yERnDPyaNnWY) in Colab, use **File > Download > Download .ipynb** to save it locally, then import it into Jupyter Lab (**File > Open**) and open it.

## Colab instructions

> [!NOTE]
> Colab is provided as a fallback if Codespaces or a local install aren't working for you. It can be slower to re-start, so use it only if the other options aren't available.

[Open the notebook in Colab](https://colab.research.google.com/drive/1zgoqilNJAMf0frdSzJ71yERnDPyaNnWY)


## Next Steps

Once you've completed the notebook, take a look at the rest of the [PyChaste tutorials](https://chaste.github.io/pychaste/tutorials/):
