-python pylance,formatblock（自动保存，格式化快捷键）, 设置自动加括号和main提示词快速生成（https://zhuanlan.zhihu.com/p/10815070274）


VSCode Markdown 插件

个人习惯推荐直接用Typora，VSCode 安装一个预览插件就可以



VSCode 排版 python 插件

代码格式化快捷键

**代码格式化，保存时自动格式化**

实现vs code中代码格式化快捷键：【Shift】+【Alt】+F

实现保存时自动代码格式化：

1）文件 ------.>【首选项】---------->【设置】；

2）搜索emmet.include;

3）在settings.json下的【工作区设置】中添加以下语句：

"editor.formatOnType": true；"editor.formatOnSave": true


## Python VSCode 格式化代码插件Pylance Black简介

在编程过程中，代码的格式化是非常重要的。良好的代码格式可以提高代码的可读性，减少错误发生的机会，并使代码更易于维护。为了方便开发者对Python代码进行格式化，VSCode提供了多个插件，本文将介绍其中几个常用的插件。

### Pylance

Pylance 是 Microsoft 开发的一款强大的 Python 语言服务器插件。它提供了多种代码格式化功能，包括自动缩进、空格和换行符的调整，以及自动对齐等功能。

Pylance 的格式化功能非常简单易用。只需在 Visual Studio Code 中将代码文件打开，并使用快捷键 `Shift + Alt + F`，或者在右键菜单中选择 “Format Document”，即可对整个文件进行格式化。Pylance 还支持对选定的代码块进行格式化，只需将代码块选中后再使用格式化快捷键即可。

以下是一个简单的示例代码：

```python
def hello(name):
    print("Hello, " + name + "!")
1.2.
```

使用 Pylance 格式化后的代码如下所示：

```python
def hello(name):
    print("Hello, " + name + "!")
1.2.
```

### Black

Black 是一个由 Python 社区开发的代码格式化工具。它遵循一系列严格的代码格式规范，可以自动对 Python 代码进行格式化，并保持代码风格的一致性。

在 VSCode 中使用 Black 插件进行代码格式化非常简单。首先，需要在系统中安装 Black 工具。然后，在 VSCode 中打开代码文件，并按下快捷键 `Ctrl + Shift + P`，在命令面板中输入 “Black: Format File”，并选择对应的命令，即可对整个文件进行格式化。如果只想格式化选定的代码块，可以选择 “Black: Format Selection” 命令。

以下是一个示例代码：

```python
def hello(name):
    print( "Hello, " + name + "!" )
1.2.
```

使用 Black 格式化后的代码如下所示：

复制[]( "一键下载全文代码")

```python
def hello(name):
    print("Hello, " + name + "!")
```



# vscode快速输入python main函数和各种代码片段方法


vscode启动快，输入速度快，但代码提示度不足，如果使用AI也会卡一下，最好把常用代码片段保存在内置中。

每次输入main函数很麻烦，需要一种快速输入，可以配置输入代码片段方法，设置如下：

![](https://pica.zhimg.com/v2-d5de16556c3f6c9aa2d951a40f329e78_1440w.jpg)

找到[python.json](https://zhida.zhihu.com/search?content_id=251185769&content_type=Article&match_order=1&q=python.json&zhida_source=entity)(可以输入找到）

![](https://pica.zhimg.com/v2-9a5c335818244a0aeb495630f4e1db54_1440w.jpg)

然后编辑输入下面的内容。

经过收集，已经包括大多数日常需要的代码片段：

我的python.json内容如下，包括日常代码片段和pandas,numpy这两个常用库的代码，这样输入起来会很快捷。

只要打出prefix的英文部分，就能出来提示，然后生成代码片段。

能提升编程效率，同时不需要记很多用法。

刚开始时，需要学习一下常用英文前缀使用，后面越用越快。

```json
{
    "Python main function": {
        "prefix": "main",
        "body": [
            "if __name__ == '__main__':",
            "    ${1:# Your code here}"
        ],
        "description": "Create a Python main function block."
    },
    "For loop": {
        "prefix": "for",
        "body": [
            "for ${1:item} in ${2:iterable}:",
            "    ${3:# Your code here}"
        ],
        "description": "Create a for loop."
    },
    "While loop": {
        "prefix": "while",
        "body": [
            "while ${1:condition}:",
            "    ${2:# Your code here}"
        ],
        "description": "Create a while loop."
    },
    "Try Except": {
        "prefix": "try",
        "body": [
            "try:",
            "    ${1:# Code that may raise an exception}",
            "except ${2:ExceptionType} as ${3:e}:",
            "    ${4:# Handle the exception}",
            "else:",
            "    ${5:# Optional else block}",
            "finally:",
            "    ${6:# Cleanup code}"
        ],
        "description": "Create a try-except block."
    },
    "Function definition": {
        "prefix": "def",
        "body": [
            "def ${1:function_name}(${2:parameters}):",
            "    \"\"\"",
            "    ${3:Description}",
            "    \"\"\"",
            "    ${4:# Your code here}",
            "    return ${5:value}"
        ],
        "description": "Create a function definition."
    },
    "Class definition": {
        "prefix": "class",
        "body": [
            "class ${1:ClassName}:",
            "    \"\"\"",
            "    ${2:Description}",
            "    \"\"\"",
            "    def __init__(self, ${3:args}):",
            "        ${4:# Initialize attributes}",
            "        pass",
            "",
            "    def ${5:method}(self, ${6:params}):",
            "        \"\"\"",
            "        ${7:Method description}",
            "        \"\"\"",
            "        ${8:# Method body}",
            "        pass"
        ],
        "description": "Create a class definition."
    },
    "Import module": {
        "prefix": "import",
        "body": [
            "import ${1:module_name}"
        ],
        "description": "Import a module."
    },
    "From import": {
        "prefix": "from",
        "body": [
            "from ${1:module_name} import ${2:names}"
        ],
        "description": "Import specific names from a module."
    },
    "List comprehension": {
        "prefix": "listcomp",
        "body": [
            "[${1:expr} for ${2:item} in ${3:iterable}]"
        ],
        "description": "Create a list comprehension."
    },
    "Dictionary comprehension": {
        "prefix": "dictcomp",
        "body": [
            "{${1:key}: ${2:value} for ${3:item} in ${4:iterable}}"
        ],
        "description": "Create a dictionary comprehension."
    },
    "Lambda function": {
        "prefix": "lambda",
        "body": [
            "lambda ${1:parameters}: ${2:expr}"
        ],
        "description": "Create a lambda function."
    },
    "Logging setup": {
        "prefix": "logsetup",
        "body": [
            "import logging",
            "logging.basicConfig(level=logging.${1:DEBUG}, format='${2:%(asctime)s - %(name)s - %(levelname)s - %(message)s}')",
            "logger = logging.getLogger(${3:'${TM_FILENAME_BASE}'})"
        ],
        "description": "Setup basic configuration for logging."
    },
    "Docstring skeleton": {
        "prefix": "docstr",
        "body": [
            "\"\"\"",
            "${1:Short description}",
            "",
            "${2:Long description}",
            "",
            "Args:",
            "    ${3:arg1 (type): Description.}",
            "Returns:",
            "    ${4:type: Description.}",
            "\"\"\""
        ],
        "description": "Create a docstring skeleton for functions or methods."
    },
    "Command line arguments": {
        "prefix": "cmdargs",
        "body": [
            "import argparse",
            "parser = argparse.ArgumentParser(description=${1:'${TM_FILENAME_BASE} script'})",
            "parser.add_argument('--${2:option}', type=${3:type}, help='${4:Help text}')",
            "args = parser.parse_args()"
        ],
        "description": "Parse command line arguments with argparse."
    },
    "Unpacking sequence into variables": {
        "prefix": "unpack",
        "body": [
            "a, b, c = [${1:item1}, ${2:item2}, ${3:item3}]"
        ],
        "description": "Unpack a sequence into multiple variables."
    },
    "Context manager": {
        "prefix": "with",
        "body": [
            "with ${1:context_manager} as ${2:variable}:",
            "    ${3:# Your code here}"
        ],
        "description": "Use a context manager with a 'with' statement."
    },
    "Decorators": {
        "prefix": "decorator",
        "body": [
            "@${1:decorator_function}",
            "def ${2:function_name}(${3:parameters}):",
            "    \"\"\"",
            "    ${4:Description}",
            "    \"\"\"",
            "    ${5:# Your code here}",
            "    return ${6:value}"
        ],
        "description": "Apply a decorator to a function."
    },
    "Property method": {
        "prefix": "prop",
        "body": [
            "class ${1:ClassName}:",
            "    @property",
            "    def ${2:property_name}(self):",
            "        \"\"\"",
            "        ${3:Description}",
            "        \"\"\"",
            "        return self._${4:attribute}",
            "",
            "    @${2:property_name}.setter",
            "    def ${2:property_name}(self, value):",
            "        \"\"\"",
            "        ${5:Setter description}",
            "        \"\"\"",
            "        self._${4:attribute} = value"
        ],
        "description": "Create a property method."
    },
    "Dataclasses": {
        "prefix": "dataclass",
        "body": [
            "from dataclasses import dataclass",
            "@dataclass",
            "class ${1:ClassName}:",
            "    ${2:field1}: ${3:type}",
            "    ${4:field2}: ${5:type} = None"
        ],
        "description": "Define a dataclass."
    },
    "Async function": {
        "prefix": "asyncdef",
        "body": [
            "async def ${1:function_name}(${2:parameters}):",
            "    \"\"\"",
            "    ${3:Description}",
            "    \"\"\"",
            "    ${4:# Your code here}",
            "    return ${5:value}"
        ],
        "description": "Create an async function."
    },
    "Async context manager": {
        "prefix": "asyncwith",
        "body": [
            "async with ${1:async_context_manager} as ${2:variable}:",
            "    ${3:# Your code here}"
        ],
        "description": "Use an async context manager with an 'async with' statement."
    },
    "Generator function": {
        "prefix": "generator",
        "body": [
            "def ${1:function_name}(${2:parameters}):",
            "    \"\"\"",
            "    ${3:Description}",
            "    \"\"\"",
            "    for item in ${4:iterable}:",
            "        yield item"
        ],
        "description": "Create a generator function."
    },
    "Iterator class": {
        "prefix": "iterator",
        "body": [
            "class ${1:IteratorName}:",
            "    def __init__(self, ${2:data}):",
            "        self._data = ${2:data}",
            "        self._index = 0",
            "",
            "    def __iter__(self):",
            "        return self",
            "",
            "    def __next__(self):",
            "        if self._index < len(self._data):",
            "            result = self._data[self._index]",
            "            self._index += 1",
            "            return result",
            "        raise StopIteration"
        ],
        "description": "Create an iterator class."
    },
    "Custom exception": {
        "prefix": "exception",
        "body": [
            "class ${1:CustomError}(Exception):",
            "    \"\"\"",
            "    ${2:Description}",
            "    \"\"\"",
            "    def __init__(self, message):",
            "        super().__init__(message)"
        ],
        "description": "Create a custom exception."
    },
    "Read file": {
        "prefix": "readfile",
        "body": [
            "with open('${1:filename}', 'r') as file:",
            "    ${2:# Your code here}",
            "    data = file.read()",
            "    ${3:# Use data}"
        ],
        "description": "Read a file."
    },
    "Write file": {
        "prefix": "writefile",
        "body": [
            "with open('${1:filename}', 'w') as file:",
            "    ${2:# Your code here}",
            "    file.write(${3:'content'})"
        ],
        "description": "Write to a file."
    },
    "Append to file": {
        "prefix": "appendfile",
        "body": [
            "with open('${1:filename}', 'a') as file:",
            "    ${2:# Your code here}",
            "    file.write(${3:'content'})"
        ],
        "description": "Append content to a file."
    },
    "Unittest setup": {
        "prefix": "unittest",
        "body": [
            "import unittest",
            "",
            "class Test${1:ClassName}(unittest.TestCase):",
            "    def setUp(self):",
            "        ${2:# Setup code}",
            "    ",
            "    def tearDown(self):",
            "        ${3:# Teardown code}",
            "    ",
            "    def test_${4:function_name}(self):",
            "        ${5:# Test code}",
            "        self.assertEqual(${6:expr1}, ${7:expr2})",
            "",
            "if __name__ == '__main__':",
            "    unittest.main()"
        ],
        "description": "Setup a unittest framework for testing."
    },
    "Thread function": {
        "prefix": "thread",
        "body": [
            "import threading",
            "",
            "def ${1:thread_function}(${2:parameters}):",
            "    \"\"\"",
            "    ${3:Description}",
            "    \"\"\"",
            "    ${4:# Your code here}",
            "",
            "thread = threading.Thread(target=${1:thread_function}, args=(${2:args}))",
            "thread.start()",
            "thread.join()"
        ],
        "description": "Create and start a new thread."
    },
    "Process function": {
        "prefix": "process",
        "body": [
            "import multiprocessing",
            "",
            "def ${1:process_function}(${2:parameters}):",
            "    \"\"\"",
            "    ${3:Description}",
            "    \"\"\"",
            "    ${4:# Your code here}",
            "",
            "process = multiprocessing.Process(target=${1:process_function}, args=(${2:args}))",
            "process.start()",
            "process.join()"
        ],
        "description": "Create and start a new process."
    },
    "Regular expression match": {
        "prefix": "regexmatch",
        "body": [
            "import re",
            "pattern = r'${1:pattern}'",
            "string = '${2:string}'",
            "match = re.match(pattern, string)",
            "if match:",
            "    ${3:# Match found}",
            "else:",
            "    ${4:# No match}"
        ],
        "description": "Match a regular expression pattern against a string."
    },
    "Regular expression search": {
        "prefix": "regexsearch",
        "body": [
            "import re",
            "pattern = r'${1:pattern}'",
            "string = '${2:string}'",
            "match = re.search(pattern, string)",
            "if match:",
            "    ${3:# Match found}",
            "else:",
            "    ${4:# No match}"
        ],
        "description": "Search a string for a regex pattern."
    },
    "Regular expression findall": {
        "prefix": "regexfindall",
        "body": [
            "import re",
            "pattern = r'${1:pattern}'",
            "string = '${2:string}'",
            "matches = re.findall(pattern, string)",
            "${3:# Process matches}"
        ],
        "description": "Find all occurrences of a regex pattern in a string."
    },
    "Virtual environment creation": {
        "prefix": "venv",
        "body": [
            "python -m venv ${1:env_name}",
            "${2:# Activate the virtual environment}",
            "${3:# Windows: .\\${1:env_name}\\Scripts\\activate}",
            "${4:# Unix or MacOS: source ${1:env_name}/bin/activate}"
        ],
        "description": "Create and activate a Python virtual environment."
    },
    "Install package via pip": {
        "prefix": "pipinstall",
        "body": [
            "pip install ${1:package_name}"
        ],
        "description": "Install a Python package using pip."
    },
    "List installed packages": {
        "prefix": "pipfreeze",
        "body": [
            "pip freeze"
        ],
        "description": "List all installed Python packages."
    },
    "Check if an object is iterable": {
        "prefix": "isiterable",
        "body": [
            "try:",
            "    iter(${1:obj})",
            "except TypeError:",
            "    ${2:# Not iterable}",
            "else:",
            "    ${3:# Iterable}"
        ],
        "description": "Check if an object is iterable."
    },
    "Flatten nested list": {
        "prefix": "flatten",
        "body": [
            "from itertools import chain",
            "flattened_list = list(chain.from_iterable(${1:nested_list}))"
        ],
        "description": "Flatten a list of lists into a single list."
    },
    "Deep copy of an object": {
        "prefix": "deepcopy",
        "body": [
            "import copy",
            "deep_copied_object = copy.deepcopy(${1:original_object})"
        ],
        "description": "Create a deep copy of an object."
    },
    "Shallow copy of an object": {
        "prefix": "shallowcopy",
        "body": [
            "import copy",
            "shallow_copied_object = copy.copy(${1:original_object})"
        ],
        "description": "Create a shallow copy of an object."
    },
    "JSON parse": {
        "prefix": "jsonparse",
        "body": [
            "import json",
            "data = json.loads('${1:json_string}')"
        ],
        "description": "Parse a JSON string into a Python dictionary."
    },
    "JSON dump": {
        "prefix": "jsondump",
        "body": [
            "import json",
            "json_string = json.dumps(${1:python_dict})"
        ],
        "description": "Convert a Python dictionary into a JSON string."
    },
    "Environment variable access": {
        "prefix": "envvar",
        "body": [
            "import os",
            "value = os.getenv('${1:ENV_VAR_NAME}', ${2:'default_value'})"
        ],
        "description": "Access an environment variable with a default value."
    },
    "Pandas DataFrame from dictionary": {
        "prefix": "pdfromdict",
        "body": [
            "df = pd.DataFrame(${1:variables})"
        ],
        "description": "Create a pandas DataFrame from a dictionary"
    },
    "Pandas describe": {
        "prefix": "pddescribe",
        "body": [
            "df.describe()"
        ],
        "description": "Generate descriptive statistics of a pandas DataFrame"
    },
    "Pandas head": {
        "prefix": "pdhead",
        "body": [
            "df.head(${1:n=5})"
        ],
        "description": "Return the first n rows of a pandas DataFrame"
    },
    "Pandas tail": {
        "prefix": "pdtail",
        "body": [
            "df.tail(${1:n=5})"
        ],
        "description": "Return the last n rows of a pandas DataFrame"
    },
    "Pandas merge": {
        "prefix": "pdmerge",
        "body": [
            "merged_df = pd.merge(${1:left},${2:right}, on='${3:key}', how='${4:inner}')"
        ],
        "description": "Merge two pandas DataFrames based on a key"
    },
    "Pandas groupby": {
        "prefix": "pdgroupby",
        "body": [
            "grouped = df.groupby('${1:key}').${2:aggfunc}.reset_index()"
        ],
        "description": "Group pandas DataFrame by a key and perform an aggregation"
    },
    "Numpy random array": {
        "prefix": "nprand",
        "body": [
            "random_array = np.random.rand(${1:shape})"
        ],
        "description": "Create a numpy array with random values"
    },
    "Numpy identity matrix": {
        "prefix": "npidentity",
        "body": [
            "identity_matrix = np.eye(${1:n})"
        ],
        "description": "Create a numpy identity matrix"
    },
    "Numpy dot product": {
        "prefix": "npdot",
        "body": [
            "dot_product = np.dot(${1:arr1},${2:arr2})"
        ],
        "description": "Calculate the dot product of two numpy arrays"
    },
    "Numpy sum": {
        "prefix": "npsum",
        "body": [
            "sum_result = np.sum(${1:arr})"
        ],
        "description": "Calculate the sum of a numpy array"
    },
    "Numpy mean": {
        "prefix": "npmean",
        "body": [
            "mean_result = np.mean(${1:arr})"
        ],
        "description": "Calculate the mean of a numpy array"
    },
    "Numpy std deviation": {
        "prefix": "npstd",
        "body": [
            "std_deviation = np.std(${1:arr})"
        ],
        "description": "Calculate the standard deviation of a numpy array"
    },

    "Pandas import": {
        "prefix": "pdimport",
        "body": [
            "import pandas as pd"
        ],
        "description": "Import pandas with a common alias."
    },
    "Numpy import": {
        "prefix": "npimport",
        "body": [
            "import numpy as np"
        ],
        "description": "Import numpy with a common alias."
    },
    "Load CSV file into DataFrame": {
        "prefix": "pdreadcsv",
        "body": [
            "df = pd.read_csv('${1:filename}.csv')",
            "${2:# Your code here}"
        ],
        "description": "Read a CSV file into a pandas DataFrame."
    },
    "Save DataFrame to CSV file": {
        "prefix": "pdwritecsv",
        "body": [
            "df.to_csv('${1:filename}.csv', index=${2:False})",
            "${3:# Your code here}"
        ],
        "description": "Write a pandas DataFrame to a CSV file."
    },
    "DataFrame head": {
        "prefix": "pdhead",
        "body": [
            "print(df.head(${1:5}))"
        ],
        "description": "Print the first few rows of a DataFrame."
    },
    "DataFrame info": {
        "prefix": "pdinfo",
        "body": [
            "print(df.info())"
        ],
        "description": "Print a summary of DataFrame information."
    },
    "Describe DataFrame": {
        "prefix": "pddescribe",
        "body": [
            "print(df.describe())"
        ],
        "description": "Generate descriptive statistics for DataFrame columns."
    },
    "Check for missing values": {
        "prefix": "pdmissing",
        "body": [
            "print(df.isnull().sum())"
        ],
        "description": "Check for any missing values in DataFrame."
    },
    "Drop rows with missing values": {
        "prefix": "pddropna",
        "body": [
            "df_cleaned = df.dropna()"
        ],
        "description": "Remove rows containing missing values from DataFrame."
    },
    "Fill missing values": {
        "prefix": "pdfillna",
        "body": [
            "df_filled = df.fillna(${1:value})"
        ],
        "description": "Fill missing values in DataFrame with a specified value."
    },
    "Group by column": {
        "prefix": "pdgroupby",
        "body": [
            "grouped = df.groupby('${1:column}')",
            "${2:# Apply aggregation}",
            "result = grouped.${3:agg_function}()"
        ],
        "description": "Group DataFrame by one or more columns and apply an aggregation function."
    },
    "Merge DataFrames": {
        "prefix": "pdmerge",
        "body": [
            "merged_df = pd.merge(df1, df2, on='${1:key}', how='${2:left/right/inner/outer}')"
        ],
        "description": "Merge two DataFrames based on a common key."
    },
    "Concatenate DataFrames": {
        "prefix": "pdconcat",
        "body": [
            "concatenated_df = pd.concat([df1, df2], axis=${1:0/1})"
        ],
        "description": "Concatenate two DataFrames along a particular axis."
    },
    "Pivot table": {
        "prefix": "pdpivot",
        "body": [
            "pivot_table = pd.pivot_table(df, values='${1:values}', index=['${2:index_col}'], columns=['${3:column_col}'])"
        ],
        "description": "Create a pivot table from DataFrame."
    },
    "Rename columns": {
        "prefix": "pdrename",
        "body": [
            "df.rename(columns={'${1:old_name}': '${2:new_name}'}, inplace=True)"
        ],
        "description": "Rename one or more columns in DataFrame."
    },
    "Select columns": {
        "prefix": "pdselectcols",
        "body": [
            "selected_cols = df[['${1:col1}', '${2:col2}']]"
        ],
        "description": "Select specific columns from DataFrame."
    },
    "Filter rows by condition": {
        "prefix": "pdfilterrows",
        "body": [
            "filtered_df = df[df['${1:column}'] ${2:> 0}]"
        ],
        "description": "Filter rows based on a condition."
    },
    "Sort DataFrame": {
        "prefix": "pdsort",
        "body": [
            "sorted_df = df.sort_values(by='${1:column}', ascending=${2:True/False})"
        ],
        "description": "Sort DataFrame by one or more columns."
    },
    "Apply function to column": {
        "prefix": "pdapply",
        "body": [
            "df['${1:new_column}'] = df['${2:column}'].apply(lambda x: ${3:x * 2})"
        ],
        "description": "Apply a function to each element of a column."
    },
    "Create dummy variables": {
        "prefix": "pddummies",
        "body": [
            "dummies = pd.get_dummies(df['${1:column}'])",
            "df = pd.concat([df, dummies], axis=1)"
        ],
        "description": "Create dummy variables (one-hot encoding) for a categorical column."
    },
    "Numpy array creation": {
        "prefix": "nparray",
        "body": [
            "arr = np.array(${1:[1, 2, 3]})"
        ],
        "description": "Create a numpy array."
    },
    "Numpy zeros array": {
        "prefix": "npzeros",
        "body": [
            "zeros_arr = np.zeros(${1:shape})"
        ],
        "description": "Create a numpy array filled with zeros."
    },
    "Numpy ones array": {
        "prefix": "npones",
        "body": [
            "ones_arr = np.ones(${1:shape})"
        ],
        "description": "Create a numpy array filled with ones."
    },
    "Numpy linspace": {
        "prefix": "nplinspace",
        "body": [
            "linspace_arr = np.linspace(${1:start}, ${2:stop}, ${3:num=50})"
        ],
        "description": "Create a numpy array with evenly spaced values over a specified interval."
    },
    "Numpy arange": {
        "prefix": "np.arange",
        "body": [
            "arange_arr = np.arange(${1:start}, ${2:stop}, ${3:step=1})"
        ],
        "description": "Create a numpy array with evenly spaced values within a given interval."
    },
    "Numpy reshape": {
        "prefix": "npreshape",
        "body": [
            "reshaped_arr = arr.reshape(${1:new_shape})"
        ],
        "description": "Reshape a numpy array."
    },
    "Numpy concatenate": {
        "prefix": "npconcat",
        "body": [
            "concatenated_arr = np.concatenate((arr1, arr2), axis=${1:0/1})"
        ],
        "description": "Concatenate two numpy arrays along a specified axis."
    },
    "Numpy std": {
        "prefix": "npstd",
        "body": [
            "standard_deviation = np.std(arr, axis=${1:None/0/1})"
        ],
        "description": "Calculate the standard deviation of array elements over a given axis."
    },
    "Numpy max": {
        "prefix": "npmmax",
        "body": [
            "maximum = np.max(arr, axis=${1:None/0/1})"
        ],
        "description": "Find the maximum value of array elements over a given axis."
    },
    "Numpy min": {
        "prefix": "npmmin",
        "body": [
            "minimum = np.min(arr, axis=${1:None/0/1})"
        ],
        "description": "Find the minimum value of array elements over a given axis."
    },
    "Numpy where": {
        "prefix": "npwhere",
        "body": [
            "filtered_arr = np.where(condition, arr1, arr2)"
        ],
        "description": "Return elements chosen from arr1 or arr2 depending on condition."
    },
    "Numpy unique": {
        "prefix": "npunique",
        "body": [
            "unique_elements = np.unique(arr, return_counts=${1:False})"
        ],
        "description": "Find the unique elements of an array."
    }
}
```
