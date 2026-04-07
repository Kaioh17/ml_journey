# `tf220` Setup Guide

This is a simple setup guide for the `tf220` Conda environment used to run `main.ipynb` with TensorFlow GPU support.

## 1. Create the environment

```bash
conda create -n tf220 python=3.10 -y
conda activate tf220
```

## 2. Install TensorFlow with CUDA support

Always use `python -m pip` inside this environment so packages go into the correct Python install.

```bash
python -m pip install --upgrade pip
python -m pip install "tensorflow[and-cuda]==2.20.0" "protobuf<6"
```

## 3. Install the notebook dependencies

These are the packages used by `main.ipynb`.

```bash
python -m pip install numpy scikit-learn keras-hub matplotlib pandas
```

Optional, but useful for Jupyter notebooks:

```bash
python -m pip install ipywidgets jupyterlab notebook
```

## 4. Verify the GPU works

Run:

```bash
python -c "import tensorflow as tf; print(tf.__version__); print(tf.config.list_physical_devices('GPU'))"
```

Expected result:

- TensorFlow version prints as `2.20.0`
- You should see something like `PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')`

## 5. Launch Jupyter

From the same environment:

```bash
jupyter lab
```

or:

```bash
jupyter notebook
```

Then open `main.ipynb`.

## 6. Recommended usage

- Activate the environment before running the notebook:

```bash
conda activate tf220
```

- Install packages with:

```bash
python -m pip install <package-name>
```

- Avoid using bare `pip`, because it may point to a different Python installation.

## 7. Common checks

Check which Python is active:

```bash
which python
python -m pip --version
```

If TensorFlow is on the GPU, notebook logs may include messages like:

- `Created device ... GPU:0`
- `Loaded cuDNN version ...`
- `Compiled cluster using XLA!`

Those are normal signs that GPU execution is working.
