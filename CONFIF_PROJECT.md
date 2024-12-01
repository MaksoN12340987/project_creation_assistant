# CONFIG PROJECT

# CMD comand

poetry init
poetry shell
mkdir src
poetry add --group lint flake8
poetry add --group lint mypy
poetry add --group lint isort
poetry add --group lint black

# Create file

__init__.py
masks.py
main.py
.flake8

# Add to file .flake8

[flake8]
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
    | dist
  )/
)
'''

[tool.isort]
line_length = 119
skip_glob = ["docs/*"]
skip = [".gitignore", ".dockerignore"]


# Add file

.gitignore

# Add to file .gitignore

# Environments
.env
.venv
env/
venv/
ENV/
env.bak/
venv.bak/

# Unit test / coverage reports
htmlcov/
.flake8
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
