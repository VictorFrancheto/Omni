# ⚙️ Environment Setup

This guide explains how to configure the project environment using either the provided **Cloud Environment** or your **Local Machine**.

## ☁️ Cloud Environment

### 1. Start the Cloud Resource

At the top of the course page:

1. Click **Cloud Resources**.
2. Select **Start Cloud Resource**.
3. Click **Open Cloud Console**.

### 2. Open the project in VS Code

In VS Code:

1. Open the **File** menu.
2. Select **Open Folder**.
3. Open the assignment directory:

```text
/voc/work/code/project/starter/
```

### 3. Create and configure the environment

Open a terminal in VS Code and run:

```bash
python --version

cd /voc/work/code/project/starter/

pip install uv

python -m uv sync

source .venv/bin/activate

python --version
```

The second `python --version` command can be used to confirm that the Python interpreter from the virtual environment is active.

### 4. Install the application in editable mode

Install the project using editable mode:

```bash
uv pip install -e .
```

Editable mode allows changes made to the source code to be reflected immediately without reinstalling the package after every modification.

### 🔑 5. Configure credentials

Make sure you are at the root of the repository and create a `.env` file from the provided example:

```bash
cp env.example .env
```

Open `.env` and configure the required environment variables:

```env
GEMINI_API_KEY=your-gemini-api-key
USER_API_KEY=my-api-key
```

Replace `your-gemini-api-key` with your actual Gemini API key.

`USER_API_KEY` can be any value for this project. For example:

```env
USER_API_KEY=my-api-key
```

> ⚠️ **Security note:** Do not commit the `.env` file to Git. In a production application, credentials should be stored using an appropriate secrets-management solution.

It is recommended that `.env` is included in `.gitignore`:

```gitignore
.env
```

---

# 💻 Local Machine

Make sure your terminal is opened inside the project starter directory.

## 1. Install `uv`

If `uv` is not already installed:

```bash
pip install uv
```

Confirm the installation with:

```bash
uv --version
```

## 2. Create the virtual environment and install dependencies

Run:

```bash
uv sync --dev
```

This command creates the `.venv` virtual environment and installs the project dependencies, including development dependencies.

## 3. Activate the virtual environment

### Linux / macOS

```bash
source .venv/bin/activate
```

### Windows PowerShell

```powershell
.venv\Scripts\Activate.ps1
```

### Windows Command Prompt

```cmd
.venv\Scripts\activate.bat
```

After activation, verify the interpreter:

```bash
python --version
```

## 4. Install the application in editable mode

Run:

```bash
uv pip install -e .
```

This installs the application in editable mode so changes made to the source files are immediately available to the installed package.

## 🧩 5. Configure the Python interpreter in VS Code

Open the Command Palette:

* **Windows/Linux:** `Ctrl + Shift + P`
* **macOS:** `Command + Shift + P`

Then select:

```text
Python: Select Interpreter
```

Choose **Enter Interpreter Path**.

### Linux / macOS

```text
.venv/bin/python
```

### Windows

```text
.venv\Scripts\python.exe
```

Using the project's virtual environment as the VS Code interpreter improves imports, autocomplete, linting, debugging, and syntax analysis.

## 🔑 6. Configure credentials

From the repository root, create `.env` from `env.example`.

### Linux / macOS

```bash
cp env.example .env
```

### Windows PowerShell

```powershell
Copy-Item env.example .env
```

Alternatively:

```powershell
cp env.example .env
```

Then edit `.env`:

```env
GEMINI_API_KEY=your-gemini-api-key
USER_API_KEY=my-api-key
```

---

# 🚀 Quick Setup

## Cloud

```bash
cd /voc/work/code/project/starter/

pip install uv

python -m uv sync

source .venv/bin/activate

uv pip install -e .

cp env.example .env
```

Then configure:

```env
GEMINI_API_KEY=your-gemini-api-key
USER_API_KEY=my-api-key
```

## Local — Linux / macOS

```bash
cd path/to/starter

pip install uv

uv sync --dev

source .venv/bin/activate

uv pip install -e .

cp env.example .env
```

## Local — Windows PowerShell

```powershell
cd path\to\starter

pip install uv

uv sync --dev

.venv\Scripts\Activate.ps1

uv pip install -e .

Copy-Item env.example .env
```

---

# ✅ Verify the Environment

Check that Python is available:

```bash
python --version
```

Check `uv`:

```bash
uv --version
```

Check that the package was installed:

```bash
uv pip list
```

Your terminal should normally display the virtual environment name, for example:

```text
(.venv)
```

Once these steps are complete, the project environment is ready for development. 🚀
