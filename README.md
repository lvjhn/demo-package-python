# DEMO-PACKAGE-PYTHON 
This sample package follows the instructions 
for publishing a Python package in PyPI. 

This repository can be used as a template for building packages. 
See section `Reusing as Template` for more info on how.

## Outline 
This `README.md` file is organized as follows: 

1. Outline 
2. Full Instructions 
3. Summarized/Compact Instructions
4. Code Structure 
5. Demo Package Installation Instructions
6. Reusing as Template
7. Adding Additional Files

## Full Instructions 
Full instructions for publishing a Python package using 
PyPI can be found here: 
https://packaging.python.org/en/latest/tutorials/packaging-projects/

I made a `tinyurl.com` short-link for the 
tutorial link above:

https://tinyurl.com/how-to-package-python

If you want, you can include the links above in your bookmarks.

## Summarized/Compact Instructions 
In summary, the instructions can be divided into the outline below
if you don't feel like clicking the tutorial link again and again.

Full instructions can be found in the tutorials above in case 
the summary doesn't still help in recalling the procedures.

1. Creating a package 
    1. Create package files (see code structure below for an example)
    1. Create `tests/` directory
    1. Create `pyproject.toml` with the necessary `[build-system]`, `[project]`, and `[project.urls]` options
    1. Configure metadata of project. Common metadata are shown below. For a more thorough example, see `pyproject.toml`
        1. name 
        1. version
        1. authors (must be in array format)
        1. description 
        1. readme
        1. license
        1. requires-python
        1. classifiers
    1. Create `README.md` file
    1. Create `LICENSE` file
1. Generating distribution archives 
    1. Step 1: Install `build` package 
        ```
        python3 -m pip install --upgrade build`
        ``` 
    1. Step 2: Run `python3 -m build` on the first build and successive build updates for different versions.
        * Generates a `dist/` folder for the built package
        * Puts a `.whl` and `.tar.gz` file in the dist folder for the current version.
1. Uploading the distribution archives 
    1. Install `twine`, a tool for uploading packages to different package indices. 
        ```
        python3 -m pip install --upgrade twine
        ```
    1. Upload archives under `dist`
        ```
        python3 -m twine upload --repository testpypi dist/*
        ```


## Code Structure 

```bash
demo-package-python
    dist/                           # distribution files 
    env/                            # virtual environment for the package 
    scripts/                        # scripts 
        build_pyproject_toml.py     # build pyproject_toml.py 
    src/                            # source files for the package 
    tests/                          # tests for the package 
        main.py         
    utils/  
        build.sh                    # shell script for building package
        publish.sh                  # shell script for publishing package
        setup.sh                    # shell script for setting up package
    LICENSE                         # MIT License 
    pyproject.dev.toml              # project configuration 
    pyproject.toml                  # built project configuration
    requirements.txt                # requirements list generated by pip freeze
```

## Demo Package Installation Instructions
The demo package has a simple API of 3 functions. 

* `.say_hello_world()`
* `.say_hi(name)`
* `.random_rainbow_color()` - uses the `faker` package 

To use this package: 
`pip install demo_package_python`

Then: 
```js
import demo_package_python as demo_package

print(".sayHello() => " + demo_package.say_hello_world()) 
print(".sayHi('John') => " + demo_package.say_hi('John'))
print(".randomRainbowColor() => " + demo_package.random_rainbow_color())
```
It should return the following: 
```
.say_hello() => Hello, World! 
.say_hi('John') => Hi, John!
.random_rainbow_color() => blue
```

## Reusing as Template
If you intend to reuse this package as a template for future package projects, use the following commands:

1. Clone the project:
    ```
    git clone https://github.com/lvjhn/demo-package-python [your_project]
    ``` 
1. Go to your project directory: 
    ```
    cd [your_project]
    ```
1. Edit `pyproject.dev.toml` to match your project description:
    > Make sure to edit the right file, you might accidentally 
      edit `pyproject.toml` instead. 

    > The file `pyproject.toml` is 
      automatically built from `pyproject.dev.toml` by adding the dependencies list 
      in `requirements.txt` before building.  

1. Remove contents of `src/demo_package_python`:
    ```
    rm -rf src/demo_package_python/*
    ```

1. Create `__init__.py` in `src/demo_package_python`:
    ```
    touch src/demo_package_python/__init__.py
    ```

1. Rename `src/demo_package_python` to `src/[your_project_name]`:
    ```
    mv src/demo_package_python src/[your_package_name]
    ```
1. Make sure that your have `virtualenv` installed and then run the following:
    ```
    virtualenv env 
    ```
    or 
    ```
    python3 -m venv env
    ```

1. Activate virtual environment:
    ```
    source env/bin/activate
    ``` 
    > Make sure that the virtual environment is activated
    before running the succeeding commands.

1. Run from the command line:
    ```
    bash utils/setup.sh
    ```
    > This command should install the packages on the `env/` folder and not on the default location.

1. Use the following commands to simplify building and publishing routines: 
    > Make sure to run the following commands in the virtual environment mode by running `source env/bin/activate` if you haven't yet.
    1. To Build Project 
        ```
        bash utils/build.sh
        ```
    1. To Publish Project 
        ```
        bash utils/publish.sh
        ```


