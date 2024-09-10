FROM python:3.9.17-slim-bookworm
WORKDIR /app

# 1. Install OS packages.  Doesn't depend on your source tree.
# Frequently just one RUN line (but could be more if you need
# packages that aren't in the default OS package repository).
RUN apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get upgrade -y && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y \
  build-essential unzip libxrender-dev libpq-dev

# 2. Copy _only_ the file that declares language-level dependencies.
# Repeat starting from here only if this file changes.
COPY requirements.txt .
RUN pip install -r requirements.txt

# 3. Copy the rest of the application in.  In a compiled language
# (Javascript/Webpack, Typescript, Java, Go, ...) build it.
COPY . .

# 4. Explain how to run the application.
EXPOSE 8000
CMD python manage.py migrate && \
  python manage.py runserver 0.0.0.0:8000
