# ML_Engineering_Basic_Python_Examples

```bash
# Create a new conda environment
conda create -n classification_models_py3.12 python=3.12 -y

# Activate the environment
conda activate classification_models_py3.12

# Install Jupyter Notebook and Required Packages
# Added sqlite to ensure compatibility with Python 3.12's sqlite3 module and prevent runtime import errors. 
conda install -c conda-forge \
  numpy \
  pandas \
  matplotlib \
  seaborn \
  scikit-learn \
  transformers \
  pytorch \
  datasets \
  accelerate \
  tqdm \
  ipywidgets \
  jupyterlab_widgets \
  jupyterlab \
  notebook \
  ipykernel \
  huggingface_hub \
  sqlite \
  tensorflow \
  openai

# Install the IPY kernel (Jupyter kernel) for the new environment
python -m ipykernel install --user --name classification_models_py3.12 --display-name "Python (classification_models_py3.12)"


# VS Code Access - Start Jupyter Notebook for remote access
# Requires Remote-SSH extension in VS Code and SSH access to the server and have Opened a Jupyter Notebook
# Then you will see the Kernel Icon and Drop Down Menu to select the kernel
# Upon entering the resulting URL for the kernel URL in VS Code, it changed to just 127.0.0.1
jupyter notebook --no-browser --port=8888 --ip=127.0.0.1
http://127.0.0.1:8888/tree?token=8266d6fed5f09a83bef0eb8bb93cb35ae1be4d5c8d82ac82

# Browser Access - Start Jupyter Notebook for remote access
jupyter notebook --no-browser --port=8888 --ip=0.0.0.0
```
### Misc Notebook Commands

```bash
jupyter notebook stop
jupyter notebook list  # to see running servers
taskkill /f /im python.exe  # be cautious—kills all Python procs
```
## Connect to Jupyter Notebook if using Web Browser Access
```
http://aiops1:8888/notebooks/finetune_modernbert_on_glue.ipynb
```
