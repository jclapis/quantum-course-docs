# Development Info

## Virtual Environment

The use of a Python virtual environment is highly recommended for development. You can use base Python or Anaconda to set one up.

> Note: The virtual environment only needs to be created once, but must be activated every time the terminal is started.

### Base Python

Install the latest version of [Python](https://www.python.org/downloads/)

Create a new virtual environment:

```bash
python3 -m venv .venv
```

Activate the virtual environment:

```bash
source .venv/bin/activate
```

> On Windows, run `.\.venv\Scripts\activate.bat`

Install dependencies:

```bash
pip install -r requirements.txt
```

### Anaconda

Install the latest version of [Anaconda](https://www.anaconda.com/products/individual#Downloads) or [Miniconda](https://docs.conda.io/en/latest/miniconda.html)

Create a new virtual environment:

```bash
conda create -n course-env pip
```

Activate the virtual environment:

```bash
conda activate course-env
```

Install dependencies:

```bash
pip install -r requirements.txt
```

## Course Docs

The course content is written in [Markdown](https://daringfireball.net/projects/markdown/) and built with [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/). All content is contained in `docs`, with units organized into subfolders. Each markdown file represents a single course module. The MkDocs configuration is defined in [mkdocs.yml](mkdocs.yml).

You can live-preview the docs with `mkdocs serve`, or build the static site with `mkdocs build`. The generated web files are output to the `site` directory.

### Including MathJax

The [Arithmatex](https://facelessuser.github.io/pymdown-extensions/extensions/arithmatex/) extension allows [MathJax](https://www.mathjax.org/) content to be integrated into the docs. Simply surround content with `$...$` to render it as inline MathJax, e.g., `$1 + 1 = 2$`. For display mode formulas, use `$$...$$`.

Example:

```text
$$
1 + 1 = 2
6 \cdot 7 = 42
$$
```

MathJax includes several [extensions](https://docs.mathjax.org/en/latest/input/tex/extensions/index.html) by default that allow you to do most anything you can do with LaTeX packages. For example, you can use `\ket{...}` to render a ket, or `\color{red}{...}` to change the text color. If you need to define additional macros, you can add them to [mathjax-config.js](docs/assets/js/mathjax-config.js) as described [here](https://docs.mathjax.org/en/latest/input/tex/macros.html).

### Styling Elements

Material for MkDocs provides many extensions and components that typically cover all the required functionality out-of-the-box. Browse out the reference documentation for code blocks, admonitions, and more. If more granular styling is needed, the [Attribute Lists](https://python-markdown.github.io/extensions/attr_list/) extension provides a syntax to set the HTML attributes on Markdown content. This is very powerful when combined with [custom CSS styles](docs/assets/css/custom-styles.css). For example, to center an image, apply the `.center` class by adding `{: .center }` after it.

> Per [docs](https://squidfunk.github.io/mkdocs-material/reference/images/#image-lazy-loading), it is best practice to add the `loading=lazy` attribute to images.

## Lab Exercises

The lab exercises are developed with a [Visual Studio](https://visualstudio.microsoft.com/vs/). To open the solution file, install the latest version of Visual Studio Community and then double-click on [Intro to Quantum Software Development.sln](exercises/Intro to Quantum Software Development.sln). (You may be able to open the solution with [Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/), but we have not tested this.)

> When installing Visual Studio, make sure the .NET Core cross-platform development workload is enabled.

In general, the exercises work by providing blank functions or operations that are validated by unit tests. Students run the test suite to check if their implementations are correct. Visual Studio shows the results in the [Test Explorer](https://docs.microsoft.com/en-us/visualstudio/test/run-unit-tests-with-test-explorer?view=vs-2019), so students get visual and immediate feedback, as well as a method to debug their code.

### Q&#35; Exercises

The Q# exercises are contained in the [QSharpExercises Q# Test Project](exercises/QSharpExercises). The project requires the .NET Core cross-platform development workload enabled in Visual Studio, and the [Microsoft Quantum Development Kit extension](https://marketplace.visualstudio.com/items?itemName=quantum.DevKit) installed. [Click here](https://docs.microsoft.com/en-us/azure/quantum/user-guide/testing-debugging?tabs=tabid-vs2019) for more information about writing unit tests for Q#.

Q# code should follow Microsoft's [style guide](https://docs.microsoft.com/en-us/azure/quantum/contributing-style-guide?tabs=guidance).

## Updating Dependencies

### Python

List outdated packages:

```bash
pip list --outdated
```

Update package:

```bash
pip install [package_name] --upgrade
```

Update [requirements.txt](requirements.txt):

```bash
pip freeze > requirements.txt
```

## CI/CD

This project uses [GitLab CI/CD](https://docs.gitlab.com/ee/ci/) to build the docs and serve them on [GitLab Pages](https://docs.gitlab.com/ee/user/project/pages/). The CI pipeline is defined in [.gitlab-ci.yml](.gitlab-ci.yml).
