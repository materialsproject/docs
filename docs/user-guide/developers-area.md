# Developer's Area

## Welcome

Welcome to the Materials Project Developer's Area.
This page describes how to develop your own applications using the data and software of the Materials Project.

## Programming language

Although you can use any programming language to develop applications, we recommend the Python programming language (version 3.0 or newer).
Python is the language of the Materials Project codebases, is widely used and supported by the scientific community, and allows for rapid development.
If you choose not to use Python, we suggest a language with good JSON parsing support (JSON is the data exchange format of the Materials Project).
In addition, we suggest a language that can easily make requests to web servers and fetch responses as JSON.

## Programming environment

If you are programming in Python, we suggest using a Python IDE such as PyCharm (commercial) or Eclipse+PyDev (free).
However, some people prefer to use a UNIX-style text editor such as vi or emacs.

## Getting and analyzing data using pymatgen

The Materials Project provides an open-source Python code, pymatgen (Python Materials Genomics), that can be used to:

- Access Materials Project data
- Convert data between several file formats
- Perform materials analyses
- Set up calculations
  The pymatgen documentation provides many examples on how to perform common tasks.
  For example, this [gist](https://gist.github.com/shyuep/3570304) by Shyue Ping Ong demonstrates how to generate phase diagrams dynamically using Materials Project data, as well as check a new material's stability with respect to decomposition.

To get started with pymatgen, we suggest you visit the [official pymatgen documentation](http://pymatgen.org/).

## Accessing Materials Project data from any program

With the Materials API, you can get Materials Project data from any program that can perform a GET request to our server.
To get started:

1. Generate an API key in your profile page.

- Log into the Materials Project web site (top-right)
- Click 'profile' (top-right)
- In the section labeled 'API key', click 'regenerate key'.
  This is your API key (copy it).
- Click 'Save Settings' (your API key will not work until this is done)

2. Make a GET request to a valid URL, for example: `https://www.materialsproject.org/rest/v1/materials/C/vasp/density?API_KEY=YOUR_API_KEY`

- (make sure you replace the text YOUR_API_KEY with your Materials Project API key)
- You should see a JSON-formatted response that includes the density of the material.
  A simple description of the Materials API [can be found here](http://www.materialsproject.org/open#) (click the 'Materials API' button).
  For more details, see our documentation on The Materials API.

## Automating calculations using FireWorks

FireWorks is an open-source Python code developed by the Materials Project for automating calculations over supercomputing clusters.
More information, including download links, is at <http://pythonhosted.org/FireWorks>
