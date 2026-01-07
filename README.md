# VFScanner

A project using the [virtual-scanner](https://github.com/imr-framework/virtual-scanner) package for MRI simulations.

## Installation

This project uses [uv](https://docs.astral.sh/uv/) for dependency management. Virtual-scanner has some compatibility requirements that need to be handled carefully.

### macOS (Apple Silicon/ARM64)

1. **Install uv** if you haven't already:
   ```bash
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```

2. **Clone or navigate to this project directory**:
   ```bash
   git clone https://github.com/sckott/vfscanner.git
   cd vfscanner
   ```

3. **Install dependencies**:
   ```bash
   uv sync
   ```

   This will automatically:
   - Use Python 3.9 (as specified in `.python-version`)
   - Install `virtual-scanner` and all its dependencies
   - Install `tensorflow-macos` (the ARM64-optimized TensorFlow variant for Apple Silicon)

   (note: if port 5000 is in use, you may see an address error, which is normal).

### Windows

1. **Install uv** if you haven't already:
   
   Download and run the installer from [uv's installation page](https://docs.astral.sh/uv/getting-started/installation/), or if you have Python installed:
   
   ```bash
   # On the command line
   pip install uv
   ```

2. **Navigate to this project directory**:
   ```bash
   # On the command line
   git clone https://github.com/sckott/vfscanner.git
   cd vfscanner
   ```

3. **Install dependencies**:
   ```bash
   # On the command line
   uv sync
   uv pip install tensorflow
   ```

   This will:
   - Download and use Python 3.9 (Windows x64 builds are available)
   - Install `virtual-scanner` and all its dependencies
   - Install `tensorflow` with the Intel/Windows-optimized variant
   - Create a virtual environment in `.venv`

   You should see the virtualscanner help output (note: if port 5000 is in use, you may see an address error, which is normal).

### Why Python 3.9?

The original virtual-scanner documentation mentions Python 3.6, but modern versions (2.0.0+) depend on TensorFlow 2.13, which requires Python 3.7+ for basic support and Python 3.9+ for optimal compatibility with all platforms.

### Troubleshooting

**Issue: "Port 5000 is already in use"**
- This is normal - virtualscanner tries to start a Flask server on port 5000
- To use a different port, you can modify the code or run with environment variables

**Issue: "No module named 'tensorflow'"**
- Make sure you ran `uv sync` successfully
- On macOS, verify that `tensorflow-macos` is installed: `uv pip list | grep tensorflow`
- On Windows, verify that `tensorflow` is installed: `uv pip list | grep tensorflow`

**Issue: Python version mismatch**
- The `.python-version` file specifies Python 3.9
- uv will automatically use this version when you run `uv sync`
- To explicitly specify a different version: `uv sync --python 3.9`

## Usage

Run this on the command line:

```bash
uv run virtualscanner
```

If the above command works you should see a url like `http://127.0.0.1:5000` - navigate to that url in your browser and you should see the application.

## Project Structure

- `.python-version` - Specifies Python 3.9 as the project's Python version
- `pyproject.toml` - Project configuration and dependency specifications
- `.venv/` - Virtual environment (created by uv, not included in git)
- `uv.lock` - Lock file with pinned dependency versions
