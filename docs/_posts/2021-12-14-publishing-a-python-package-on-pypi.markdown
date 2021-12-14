---
layout: post
title:  "Publishing a python package on PyPi"
date:   2021-12-16 20:15:00 +0100
categories: python, package, pypi
---

I am going to demonstrate in 5 easy steps how to publish a Python package on PyPi with a small example project.

# 1. Structure your code correclty
- Create a new Python project, I call it "packaging_tutorial"
- Inside this project, create two folders named "dist" and "src"
- Inside the src folder, create a new folder called "example package". This is the package that I will publish on PyPi.

# 2. Create & configure config files
- Create two files, pyproject.toml & setup.cfg, in the root directory of our Python project "packaging_tutorial". 
I included example configs below. 

For all available options & keys, look 
- (here)[https://setuptools.pypa.io/en/latest/userguide/declarative_config.html] for setup.cfg 
- and (here)[https://setuptools.pypa.io/en/latest/build_meta.html] for pyproject.toml

setup.cfg
```
[metadata]
name = example_package
version = 0.0.1
author = Tim Fischer
author_email = tim.s.fischer96@googlemail.com
description = An example package.
long_description = file: README.md
long_description_content_type = text/markdown
url = https://github.com/example/package
project_urls =
    Bug Tracker = https://github.com/example/package/issues
classifiers =
    Programming Language :: Python :: 3
    License :: OSI Approved :: Apache Software License

[options]
package_dir =
    = src
packages = find:
python_requires = >=3.6
install_requires =
    jsonnet
    allennlp==2.1.0
    allennlp-models==2.1.0
    transformers
    stanza
    sentence_transformers

[options.packages.find]
where = src
```

pyproject.toml
```
[build-system]
requires = [
    "setuptools>=42",
    "wheel"
]
build-backend = "setuptools.build_meta"
```

# 3. Install python build dependency
To build a project, we need to install the build package and twine for uploading as follows:
```
$ python3 -m pip install --upgrade build
$ python3 -m pip install --upgrade twine
```

# 4. Build the project
Now, we can build our project. This will create two files in the dist directory: a .tar.gz and a .whl file.
```
$ python3 -m build
```

# 5. Upload the package to PyPi
Finally, we can upload the package to the Python Packaging Index. Here we have two options, uploading the project to the test instance (testpypi) or to the real instance. I recommend to upload the project to the test instance first, check if everything works as expected and then, upload it to the real PyPi.
```
Upload to testpypi
python3 -m twine upload --repository testpypi dist/*

Upload to PyPi
python3 -m twine upload dist/*
```
You can now visit the example package:
- View at Pypi: [https://pypi.org/project/example-pkg-bigabig/0.0.1/](https://pypi.org/project/example-pkg-bigabig/0.0.1/)
- View at testpypi: [https://test.pypi.org/project/example-pkg-bigabig/0.0.1/](https://test.pypi.org/project/example-pkg-bigabig/0.0.1/)

# (Optional) Install your package
You can now install your package easily!
```
Install from testpypi:
$ pip install --index-url https://test.pypi.org/simple/ example-pkg-bigabig

Install from pypi:
$pip install example-pkg-bigabig
```
