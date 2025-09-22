# Installation and Project SetUp

### 1. Virtual Environment Creation

```bash
python3 -m venv env
```

On Linux or macOS:

```bash
source env/bin/activate
```

On Windows:

```bash
env\Scripts\activate
```
### 2. Directory Structure

At this point, your directory structure should look like this:

```
└── env
```

### 3. Installing FastAPI

```console
(env) pip install "fastapi[standard]"
```

### 4. Freeze Dependencies

```console
(env) pip freeze > requirements.txt
```

### 5. Confirm the installation

```python
(env) fastapi --version
FastAPI CLI version: 0.0.2
```