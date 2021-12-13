FROM alpine/git:v2.32.0 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/PetterS/realtimechess.git /app
WORKDIR /app
RUN git checkout a24c109af441454b1c678e9906f31cec9ba56b7b
RUN rm -rf .git


FROM python:3.10.1-slim
WORKDIR /app
EXPOSE 8080
ENV POETRY_VERSION=1.0.0
RUN pip install "poetry==$POETRY_VERSION"
COPY --from=clone /app/poetry.lock /app/pyproject.toml /app/
RUN poetry config virtualenvs.create false && \
    poetry install --no-dev --no-interaction --no-ansi
COPY --from=clone /app /app
CMD ["python3", "realtimechess.py", "run"]
