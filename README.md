# Django Quiz Web App

A server-rendered quiz and exam application built with Django. It supports
categorized quizzes, configurable pass marks, randomized questions, single
attempts, progress tracking, stored exam sittings, staff marking, and CSV-based
user import. Content and questions are managed through Django's admin site.

## Project status

This is a historical Django 2.2 project, not a production-ready service. Its
pinned framework version is no longer supported, and the checked-in settings
enable debug mode and contain a development secret key. Use an isolated,
disposable environment for study or local evaluation; review and modernize the
application before exposing it to a network.

## What is included

- `quiz/`: quiz, category, question, sitting, progress, marking, and CSV import
  models and views
- `mcq/`: multiple-choice question support
- `online_test/`: project URLs, settings, and WSGI entry point
- SQLite as the default local database
- Django admin at `/admin/`

The repository does not contain starter quiz data. Create an administrator and
add categories, quizzes, and questions in the admin before using the quiz flow.

## Local setup

The dependency pins target the Python/Django ecosystem of 2020. Python 3.8 is a
practical compatibility choice for the pinned Django 2.2 release.

```bash
git clone https://github.com/khlaifiabilel/django-quiz-web-app.git
cd django-quiz-web-app
python3.8 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

Open <http://127.0.0.1:8000/> for the application or
<http://127.0.0.1:8000/admin/> to create content. `migrate` is sufficient for a
fresh checkout because application migrations are already committed; do not run
`makemigrations` as an installation step.

## Checks

With compatible dependencies installed:

```bash
python manage.py check
python manage.py test
```

The checked-in test modules contain no substantive test cases, so a successful
test command is primarily an import and configuration check.

## Configuration and security

`online_test/settings.py` is development configuration:

- `SECRET_KEY` is committed and must not be reused for a deployment.
- `DEBUG` is `True` and `ALLOWED_HOSTS` is empty.
- Uploaded question figures and CSV files require a deliberate media-serving
  and storage configuration outside Django's development server.
- CSV import creates users from file contents, including passwords. Treat input
  files as sensitive and review that workflow before use.
- SQLite is suitable for local evaluation, not a multi-user production setup.

Move secrets and deployment-specific values to environment-backed settings,
disable debug mode, configure allowed hosts and media storage, and run Django's
deployment checks before considering deployment.

## Provenance

This repository's Git history begins with an import by `kalifiabillal` on
2021-02-21. The quiz implementation derives from the configurable
[`tomwalker/django_quiz`](https://github.com/tomwalker/django_quiz) codebase via
the related [`sswapnil2/django-quiz-app`](https://github.com/sswapnil2/django-quiz-app)
project; class names and the historical setup reference preserve that lineage.
Later code in this repository adds CSV-driven user creation. This repository is
not marked as a GitHub fork, so that relationship is not represented by GitHub's
fork metadata.

## Known limitations

- Django 2.2 and `django-model-utils` 3.1 are obsolete dependency lines.
- There is no deployment configuration, package release, or supported hosted
  instance.
- CSV parsing assumes a specific comma/semicolon layout and has limited error
  handling.
- Automated behavioral coverage is effectively absent.

## License

This repository includes an [MIT License](LICENSE). The identified imported
projects have no detected license, so this declaration should not be read as
relicensing material for which the repository owner does not hold the necessary
rights. Verify provenance and applicable terms before reusing imported source.
Dependencies retain their respective licenses.
