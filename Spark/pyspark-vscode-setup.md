
# 🧠 PySpark Setup Guide for VS Code on Mac M3 (JDK 17 & Python Preinstalled)

This guide helps you set up PySpark development **completely inside VS Code**, assuming you already have:
- ✅ Homebrew
- ✅ Python installed
- ✅ JDK 17 installed

---

## ✅ Step 1: Confirm Java & Python

In the VS Code terminal:

```bash
java -version
python3 --version
```

Ensure Java environment variable is set:

```bash
echo 'export JAVA_HOME=$(/usr/libexec/java_home)' >> ~/.zshrc
source ~/.zshrc
```

Check:
```bash
echo $JAVA_HOME
```

---

## ✅ Step 2: Install Apache Spark

```bash
brew install apache-spark
```

Add Spark to your environment:

```bash
echo 'export SPARK_HOME="/opt/homebrew/opt/apache-spark/libexec"' >> ~/.zshrc
echo 'export PATH="$SPARK_HOME/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

Test Spark:

```bash
spark-shell
```

✅ If you see the Scala REPL prompt, Spark is working.

**Exit the REPL** by typing `:quit` or pressing `Ctrl + D`

---

## ✅ Step 3: Set Up PySpark in a Project Folder

Create a project folder and a virtual environment:

```bash
mkdir my-pyspark-project
cd my-pyspark-project
python3 -m venv venv
source venv/bin/activate
```

Install PySpark:

```bash
pip install pyspark
```

(Optionally for notebooks):

```bash
pip install jupyterlab ipykernel
```

---

## ✅ Step 4: Configure VS Code

### 📁 4.1 Open the Folder
Open `my-pyspark-project` in VS Code.

---

### 🧩 4.2 Install Extensions

- Python
- Jupyter
- Pylance

---

### 🐍 4.3 Select the Python Interpreter

1. `Cmd + Shift + P` → `Python: Select Interpreter`
2. Choose: `./venv/bin/python`

---

### 🧪 4.4 Verify in Terminal

```bash
which python
```

Should return path to your `venv` like:
```
/Users/yourname/my-pyspark-project/venv/bin/python
```

Then test:
```bash
python test_spark.py
```

---

## ✅ Step 5: Example PySpark Script

Create `test_spark.py` in your folder:

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder     .appName("VSCode Test")     .getOrCreate()

df = spark.createDataFrame([
    ("Alice", 1),
    ("Bob", 2),
    ("Charlie", 3)
], ["name", "id"])

df.show()
spark.stop()
```

Run it:
```bash
python test_spark.py
```

✅ You’re ready to use PySpark in VS Code!

---

## 🧰 Optional

- Add a `.vscode/settings.json` to auto-select the interpreter
- Use Jupyter notebooks with PySpark
- Connect to real data (CSV, Parquet, DBs)

Let me know if you need help with those!
