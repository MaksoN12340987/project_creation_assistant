# CONFIG PROJECT

### Secrett data
.env
.env.txt

# CMD comand

poetry init
poetry self add poetry-plugin-shell
poetry shell
mkdir src
poetry add requests
poetry add python-dotenv
poetry add pandas

<!-- Django -->
poetry add django

<!-- Для БД -->
poetry add psycopg2

<!-- Для работы с image в Django -->
poetry add Pillow

<!-- Для excel -->
poetry add openpyxl

poetry add --group lint flake8
poetry add --group lint mypy
poetry add --group lint isort
poetry add --group lint black
poetry add --group dev pytest
poetry add --group dev pytest-cov

# Create file

"if __name__ == '__main__':" > src/main.py

# Add to file .flake8

"[flake8]" > .flake8
max-line-length = 119
ignore = E203, W503
exclude = .git, __pycache__, venv, .venv


# Add to file .toml

[tool.mypy]
disallow_untyped_defs = true
no_implicit_optional = true
warn_return_any = true
warn_unreachable = true
exclude = 'venv'

[tool.black]
line-length = 119
exclude = '''
(
  /(
      \.eggs
    | \.git
    | \.hg
    | \.mypy_cache
    | \.tox
    | \.venv
    | \.gitignore
    | dist
  )/
)
'''

[tool.isort]
line_length = 119
skip_glob = ["docs/*"]
skip = [".gitignore", ".dockerignore"]


# Add to file .gitignore

"# Environments" > .gitignore
.env
.venv
.idea
env/
venv/
ENV/
env.bak/
venv.bak/


# Byte-compiled / optimized / DLL files
__pycache__/
*.py[cod]
*$py.class

# C extensions
*.so

# Distribution / packaging
.Python
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
wheels/
share/python-wheels/
*.egg-info/
.installed.cfg
*.egg
MANIFEST

# PyInstaller
*.manifest
*.spec

# Installer logs
pip-log.txt
pip-delete-this-directory.txt

# Unit test / coverage reports
htmlcov/
.tox/
.nox/
.coverage
.coverage.*
.cache
nosetests.xml
coverage.xml
*.cover
*.py,cover
.hypothesis/
.pytest_cache/
cover/

# Translations
*.mo
*.pot

# Django stuff:
*.log
local_settings.py
db.sqlite3
db.sqlite3-journal

# Flask stuff:
instance/
.webassets-cache

# Scrapy stuff:
.scrapy

# Sphinx documentation
docs/_build/

# PyBuilder
.pybuilder/
target/

# Jupyter Notebook
.ipynb_checkpoints

# IPython
profile_default/
ipython_config.py

# pyenv

# pipenv
#Pipfile.lock

# poetry
#poetry.lock

# pdm
#pdm.lock

.pdm.toml
.pdm-python
.pdm-build/

# PEP 582; used by e.g. github.com/David-OConnor/pyflow and github.com/pdm-project/pdm
__pypackages__/

# Celery stuff
celerybeat-schedule
celerybeat.pid

# SageMath parsed files
*.sage.py

# Spyder project settings
.spyderproject
.spyproject

# Rope project settings
.ropeproject

# mkdocs documentation
/site

# mypy
.mypy_cache/
.dmypy.json
dmypy.json

# Pyre type checker
.pyre/

# pytype static type analyzer
.pytype/

# Cython debug symbols
cython_debug/



# PACKAGE_PARENT = '..'
# SCRIPT_DIR = os.path.dirname(os.path.realpath(os.path.join(os.getcwd(), os.path.expanduser(__file__))))
# sys.path.append(os.path.normpath(os.path.join(SCRIPT_DIR, PACKAGE_PARENT)))
