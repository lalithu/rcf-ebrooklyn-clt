# Mac prerequisites — inspect, then install only if needed

Codex must detect macOS architecture, Python interpreter, pip availability, Node/npm, FFmpeg, Git/GitHub CLI and cv2 import before modifying anything. Do NOT assume Homebrew. Keep dependencies isolated in analysis/.venv and replay/node_modules. Never globally upgrade or overwrite a system Python.

Typical non-destructive checks:

    uname -m
    python3 --version
    python3 -m pip --version
    python3 -c 'import cv2; print(cv2.__version__)'
    node --version
    npm --version
    ffmpeg -version
    gh auth status

If cv2 missing and user approves analysis phase, make a local venv with python3 -m venv analysis/.venv, then pip install a pinned compatible numpy/scipy/opencv-python-headless/matplotlib/pytest stack. Do not install opencv-python and opencv-python-headless concurrently. Frontend may use Vite/React/TypeScript if no reusable portfolio framework. Use package lockfile, verify GitHub Pages base path is /rcf-ebrooklyn-clt/ unless custom domain/routing changes it. Do not install or run heavy CV during UI approval gate.

Reference: https://pypi.org/project/opencv-python-headless/
