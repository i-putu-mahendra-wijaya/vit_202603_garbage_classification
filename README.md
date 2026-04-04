# Garbage Classification with ViT

Simple ViT project for the BINUS course **Deep Learning and Its Application**.

This repository contains a Jupyter notebook that:

- downloads the `asdasdasasdas/garbage-classification` dataset from Kaggle,
- performs exploratory analysis and preprocessing,
- fine-tunes a Vision Transformer (ViT) image classifier with TensorFlow and Hugging Face Transformers.

## Project Contents

- `garbage_classification.ipynb`: main notebook for the project
- `pyproject.toml`: Python dependencies managed with Poetry
- `poetry.lock`: locked dependency versions
- `dataset/`: generated local cache for downloaded image files after the notebook runs

## Supported Environment

This project is configured for:

- macOS
- Linux

The dependency file currently installs TensorFlow only on `darwin` and `linux`.

If you use Windows, use one of these options:

- run the project inside WSL2 Ubuntu, or
- run the notebook in Google Colab instead of local setup.

## Prerequisites

Install these first:

- Python `3.12.x`
- Poetry `2.x`
- Git

Recommended:

- Jupyter support in VS Code, PyCharm, or JupyterLab
- A Kaggle account for dataset download
- A Hugging Face account and token for downloading the pre-trained ViT model used in the notebook

## 1. Install Python 3.12

Check your Python version:

```bash
python3 --version
```

You should see Python `3.12.x`.

If not, install Python 3.12 first. Two common options are:

### Option A: official installer

- macOS/Windows: install Python 3.12 from python.org
- Linux: install Python 3.12 using your package manager or `pyenv`

### Option B: pyenv

If you already use `pyenv`:

```bash
pyenv install 3.12.10
pyenv local 3.12.10
python --version
```

## 2. Install Poetry

Check whether Poetry is already installed:

```bash
poetry --version
```

If it is missing, install it:

```bash
curl -sSL https://install.python-poetry.org | python3 -
```

After installation, reopen your terminal and verify again:

```bash
poetry --version
```

## 3. Clone the Repository

```bash
git clone git@github.com:i-putu-mahendra-wijaya/vit_202603_garbage_classification.git
cd vit_202603_garbage_classification
```

If your lecturer already distributed the folder, just open the project directory in your terminal.

## 4. Install Project Dependencies

Inside the project folder, run:

```bash
poetry install
```

This creates a virtual environment and installs all required packages from `pyproject.toml` and `poetry.lock`.

Important packages include:

- TensorFlow `2.16.2`
- `tensorflow-macos` on macOS
- `tensorflow-metal` on Apple Silicon Macs
- `tf-keras`
- scikit-learn
- pandas
- seaborn
- matplotlib
- huggingface-hub
- transformers
- datasets
- accelerate
- timm
- kagglehub
- ipykernel

## 5. Activate the Virtual Environment

Run:

```bash
poetry shell
```

If your Poetry version does not support `poetry shell`, use:

```bash
poetry env activate
```

Then execute the printed command in your terminal.

You can also run commands without activating the shell by prefixing them with `poetry run`.

Example:

```bash
poetry run python --version
```

## 6. Register the Jupyter Kernel

This makes the Poetry environment appear as a notebook kernel.

```bash
poetry run python -m ipykernel install --user --name garbage-classification --display-name "Python (garbage-classification)"
```

After that, open the notebook and select the kernel:

`Python (garbage-classification)`

## 7. Set Up Kaggle Authentication

The notebook downloads data from Kaggle, so authentication is required.

Create a Kaggle account if you do not have one yet:

- https://www.kaggle.com/

Then generate your API key from:

- https://www.kaggle.com/settings

There are two supported ways to authenticate.

### Option A: `kaggle.json` file

Download `kaggle.json` from Kaggle and place it here:

```bash
~/.kaggle/kaggle.json
```

Recommended permissions:

```bash
mkdir -p ~/.kaggle
chmod 700 ~/.kaggle
chmod 600 ~/.kaggle/kaggle.json
```

### Option B: access token file

The notebook also checks this path:

```bash
~/.kaggle/access_token
```

If neither file exists, `kagglehub.login()` may prompt you to log in interactively from the notebook.

## 8. Set Up Hugging Face Authentication

The notebook logs into Hugging Face before loading the pretrained ViT model.

Create a token from:

- https://huggingface.co/settings/tokens

Then create this file from the template already included in the repository:

```bash
cp cred/hf_token.json.template cred/hf_token.json
```

Edit `cred/hf_token.json` and place your token in the `value` field.

## 9. Open and Run the Notebook

Start Jupyter:

```bash
poetry run jupyter notebook
```

Or:

```bash
poetry run jupyter lab
```

Then open:

`garbage_classification.ipynb`

Run the cells from top to bottom.

What the notebook does:

1. checks available CPU/GPU devices,
2. authenticates with Kaggle,
3. downloads the dataset if needed,
4. copies JPG files into the local `dataset/` folder,
5. loads and analyzes the data,
6. trains the ViT model.

## Dataset Behavior

The notebook uses the Kaggle dataset:

- https://www.kaggle.com/datasets/asdasdasasdas/garbage-classification

When first run:

- the dataset is downloaded through `kagglehub`,
- JPG files are copied into the local `dataset/` folder.

On later runs:

- if JPG files already exist in `dataset/`, the notebook reuses them and skips downloading again.

## GPU Notes

### Apple Silicon Mac

On Apple Silicon (`arm64`) Macs, this project installs `tensorflow-metal`, which allows TensorFlow to use the Apple GPU backend.

You can verify device detection by running the first notebook cells.

### Linux

The project installs standard TensorFlow for Linux. GPU support depends on your local CUDA/cuDNN setup and is not configured automatically by this repository.

If TensorFlow does not detect a GPU, the notebook will still run on CPU.

## Common Commands

Install dependencies:

```bash
poetry install
```

Check environment:

```bash
poetry run python --version
poetry run pip list
```

Launch notebook:

```bash
poetry run jupyter notebook
```

Start JupyterLab:

```bash
poetry run jupyter lab
```

## Troubleshooting

### `python: command not found`

Use `python3` instead, or make sure your Poetry environment is active.

### `poetry: command not found`

Poetry is not installed or not on your `PATH`. Reinstall Poetry and reopen the terminal.

### Kaggle authentication fails

Check that one of these files exists:

- `~/.kaggle/kaggle.json`
- `~/.kaggle/access_token`

Also verify the file permissions, especially on macOS/Linux.

### TensorFlow installation issues

Make sure you are using Python `3.12.x`. Installing a different Python version may cause dependency resolution or binary compatibility problems.

### Kernel does not appear in Jupyter

Run the kernel registration command again:

```bash
poetry run python -m ipykernel install --user --name garbage-classification --display-name "Python (garbage-classification)"
```

## Suggested Setup

If you want the smoothest local setup:

1. install Python `3.12`
2. install Poetry
3. run `poetry install`
4. create Kaggle API credentials
5. register the Jupyter kernel
6. open `garbage_classification.ipynb` and run all cells in order

## License

This project is licensed under the MIT License. See `LICENSE`.
