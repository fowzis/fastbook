# Installation Instructions on Windows MSL
The following are the instruction to install an use fastbook notebook and JupyterLab on Windows WSL

## System Wide Setup
```bash
# Upgrade pip
sudo apt install python3 python3-pip python3-venv
sudo apt upgrade python3 python3-pip python3-venv
sudo apt install git
sudo apt autoremove

# Install cuda-toolkit
sudo apt install nvidia-cuda-toolkit
```

## Clone fastbook notebook from private fork in github
```bash
# Clone fastbook notebook
git clone https://github.com/fowzis/fastbook.git

cd fastbook

# Create a virtual environment
python -m venv fastbook-env

# Activate the virtual environment
# On Linux/macOS:
source fastbook-env/bin/activate
# On Windows:
fastbook-env\Scripts\activate

pip install --upgrade pip

# Install packages
pip install "python>=3.6"
pip install "torch>=1.6" torchvision -f https://download.pytorch.org/whl/torch_stable.html

# Install fast additional dependencies from requirements.txt
pip install -r requirements.txt
```

### Explanation:
1. The `python>=3.6` ensures the environment uses Python version 3.6 or later.
2. The `torch>=1.6` and `torchvision` are equivalent to the PyTorch dependencies specified in the `environment.yml` file. Since PyTorch often requires specific instructions for GPU support, you might need the appropriate URL from the [PyTorch website](https://pytorch.org/get-started/locally/).
3. The `requirements.txt` file dependencies are installed using `pip install -r requirements.txt`.

## PyTorch GPU Check
To check if PyTorch can utilize your GPU, you can run the following simple Python script:
While the fastbook-env virtual environment is activated, run python3 and add the following script to it or add a JupyterLab Cell with the following python code
```python
import torch

# Check if CUDA is available
if torch.cuda.is_available():
    print("CUDA is available. PyTorch can use the GPU!")
    print("GPU Name:", torch.cuda.get_device_name(0))
else:
    print("CUDA is not available. PyTorch is using the CPU.")
```
 Explanation:
1. **`torch.cuda.is_available()`**: This function checks if your system has CUDA support and if PyTorch is properly configured to use it.
2. **`torch.cuda.get_device_name(0)`**: This displays the name of the detected GPU (if available).

If you see "CUDA is available," you're good to go for GPU acceleration in PyTorch. Otherwise, you may need to verify your GPU drivers, CUDA toolkit installation, or PyTorch setup.


# Download Node.js

```bash
# Install dependency packages 
sudo apt install unzip
 
# Download and install fnm:
curl -o- https://fnm.vercel.app/install | bash

# Download and install Node.js:
fnm install 22

# Verify the Node.js version:
node -v # Should print "v22.14.0".

# Verify npm version:
npm -v # Should print "10.9.2".
```


# Installing JupyterLab

Here's how you can install, run, and use JupyterLab to open a notebook:

```bash
# Install JupyterLab
pip install jupyterlab
```

After the installation, run JupyterLab with this command:
```bash
# Launch JupyterLab
jupyter-lab
```

This will automatically open JupyterLab in your default web browser. If it doesn't, the terminal will display a URL (starting with `http://localhost:8888/`)—you can copy and paste this into your browser.

In JupyterLab:
- **To create a new notebook**: Click the **"Python [default]"** option under the "Notebook" section on the launcher screen.
- **To open an existing notebook**: Use the file browser on the left-hand side to navigate to the `.ipynb` file you want to open, and click it to launch.

You’re all set to start coding in your Jupyter notebook within the JupyterLab environment! Let me know if you hit any snags or need more tips. 🚀



## JupyterLab UI extentions 

### **1. Verify `ipywidgets` Installation**
   - Make sure you have `ipywidgets` installed in your environment:
     ```bash
     pip install ipywidgets
     ```
   - If you're using JupyterLab, also install the JupyterLab extension for `ipywidgets`:
     ```bash
     jupyter labextension install @jupyter-widgets/jupyterlab-manager
     ```
   - Restart JupyterLab after installing the extension.

### **2. Enable the Widgets Extension**
   - Verify that widgets are enabled:
     ```bash
     jupyter nbextension enable --py widgetsnbextension
     jupyter nbextension install --py widgetsnbextension
     ```

### **3. Update JupyterLab and Extensions**
   - If the issue persists, try updating JupyterLab and related extensions:
     ```bash
     pip install --upgrade jupyterlab ipywidgets
     jupyter lab build
     ```

### **4. Kernel Compatibility**
   - Ensure that the kernel in use supports interactive widgets. If you're using a custom kernel or virtual environment, install `ipywidgets` within that environment.

### **5. Debugging Display Issues**
   - If the widget still doesn't appear:
     - Add a `display(uploader)` command to explicitly render the widget:
       ```python
       from IPython.display import display
       display(uploader)
       ```
     - Check the browser console (F12 in most browsers) for errors related to JupyterLab or widgets.

### **6. Test a Simple Widget**
   - To confirm that widgets are working, try running this code:
     ```python
     import ipywidgets as widgets
     button = widgets.Button(description="Click Me!")
     display(button)
     ```
     If the button renders correctly, your setup is working fine.

Let me know how these steps go! 🛠️



Your JupyterLab server started successfully, but the system is unable to open the browser due to some missing configurations and packages. Let's address these warnings step by step:

---

### **1. Missing `mimeinfo.cache`**
   - This warning indicates that your system's MIME database isn't updated. Run the following command to update it:
     ```bash
     sudo update-desktop-database
     ```
   - If the command is unavailable, install the `desktop-file-utils` package. For Debian/Ubuntu systems:
     ```bash
     sudo apt install desktop-file-utils
     ```

---

### **2. Missing Browsers**
   - The error indicates that no compatible web browsers (like Firefox, Chrome, etc.) were found. You need to install one. For example:
     - **Install Firefox**:
       ```bash
       sudo apt update
       sudo apt install firefox
       ```
     - **Install Google Chrome**:
       Download and install the `.deb` file from the [official Chrome website](https://www.google.com/chrome/), then run:
       ```bash
       sudo dpkg -i google-chrome-stable_current_amd64.deb
       sudo apt --fix-broken install
       ```

   - After installing a browser, set it as the default browser:
     ```bash
     xdg-settings set default-web-browser firefox.desktop
     ```

---

### **3. Open JupyterLab Manually**
```bash
# Launch JupyterLab
jupyter-lab
```
   - If automatic browser launching fails, you can still manually open JupyterLab:
     1. Copy the URL from the terminal (e.g., `http://localhost:8888/lab?...`).
     2. Paste it into your browser's address bar.

---

### **4. Ensure Basic Command-Line Browsing Tools**
   - Optional: If you'd like basic tools like `lynx`, `w3m`, or `links`, you can install them:
     ```bash
     sudo apt install lynx
     sudo apt install w3m
     ```

---

These steps should fix the browser-related issues and make opening JupyterLab much smoother. Let me know if you encounter anything else! 🚀