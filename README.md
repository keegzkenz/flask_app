### Running API & DB
`docker-compose up -d --build`

### Run Flask shell
`docker-compose exec api flask shell`

### Update dev database
`docker-compose exec api python manage.py recreate_db`

### Seed dev database
`docker-compose exec api python manage.py seed_db`

### Go into dev psql
```
docker-compose exec api-db psql -U postgres

# in psql now

# connect to dev database
\c api_dev

# list relations
\dt

# quit
\q
```

`docker-compose exec api-db psql -U postgres`

### Adding python packages
1. `pip install PACKAGE_NAME`
2. `pip freeze > requirements.txt`
3. Rebuild docker images (requirements are installed at build time rather than run time): `docker-compose up -d --build`

### Testing

# run all tests
`docker-compose exec api python -m pytest "src/tests"`

# run tests and see code coverage
`docker-compose exec api python -m pytest "src/tests" -p no:warnings --cov="src" --cov-report html`
`open htmlcov/index.html` # view test coverage in browser

# disable warnings
`docker-compose exec api python -m pytest "src/tests" -p no:warnings`

# run only the last failed tests
`docker-compose exec api python -m pytest "src/tests" --lf`

# run only the tests with names that match the string expression
`docker-compose exec api python -m pytest "src/tests" -k "config and not test_development_config"`

# stop the test session after the first failure
`docker-compose exec api python -m pytest "src/tests" -x`

# enter PDB after first failure then end the test session
`docker-compose exec api python -m pytest "src/tests" -x --pdb`

# stop the test run after two failures
`docker-compose exec api python -m pytest "src/tests" --maxfail=2`

# show local variables in tracebacks
`docker-compose exec api python -m pytest "src/tests" -l`

# list the 2 slowest tests
`docker-compose exec api python -m pytest "src/tests" --durations=2`

### Linting

# run Flake8
`docker-compose exec api flake8 src`

# run Black
`docker-compose exec api black src --check` # check only

`docker-compose exec api black src  --diff` # show diff

`docker-compose exec api black src` # make changes

# run isort
`docker-compose exec api isort src --check-only` # check only

`docker-compose exec api isort src --diff` # show diff

`docker-compose exec api isort src` # apply changes