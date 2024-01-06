README
======

Deployment
----------

🔗[听溪 | Brooke's Blog](https://brookes-blog.readthedocs.io/zh/latest/)

👍Resources to build this

* [MkDocs](https://www.mkdocs.org/)
* [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
* [Read the Docs](https://readthedocs.org/)
* [giscus](https://giscus.app/)
* [GitHub](https://github.com/)

Cheatsheet
----------

### To preview locally

1. Clone the repo and go to repo directory
2. Create and activate Python environment: needs only `mkdocs` and `mkdocs-material`
    * Using Conda: miniforge3 or any other conda/mamba package manager
        1. `> conda create -n <conda_env_name> python=3.10 --no-deps`
        2. `> conda activate <conda_env_name>`
    * Using venv: python 3.10.x is required
        1. `> python -m venv <venv_path>`
        2. `source <venv_path>/bin/activate`
3. `> pip install -r requirements.txt`
4. `> mkdocs serve` to preview it locally

Using of requirements.txt is because readthedocs does not support a lot of conda versions. See [Configuration file v2 (.readthedocs.yaml) — Read the Docs user documentation](https://docs.readthedocs.io/en/stable/config-file/v2.html#build-tools-python)

### To export requirements.txt

1. Go to the repo directory
2. Activate the environment
3. `> pip freeze > requirements.txt`
