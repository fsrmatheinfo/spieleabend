FROM alpine/git:v2.26.2 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/PetterS/realtimechess.git /app
WORKDIR /app
RUN git checkout 1ecc27faef785373a78df6b2563fb9d193eece4f
RUN rm -rf .git


FROM python:3.6.12-slim
WORKDIR /app
EXPOSE 8080
ENV POETRY_VERSION=1.0.0
RUN pip install "poetry==$POETRY_VERSION"
COPY --from=clone /app/poetry.lock /app/pyproject.toml /app/
RUN poetry config virtualenvs.create false && \
    poetry install --no-dev --no-interaction --no-ansi
COPY --from=clone /app /app
CMD ["python3", "realtimechess.py", "run"]
