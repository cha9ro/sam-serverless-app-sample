FROM public.ecr.aws/docker/library/python:3.12-slim
COPY --from=public.ecr.aws/awsguru/aws-lambda-adapter:0.8.3 /lambda-adapter /opt/extensions/lambda-adapter
ENV PORT=8000
WORKDIR /var/task
RUN apt-get update && apt-get install -y \
RUN pip install --upgrade pip && pip install poetry
RUN poetry config virtualenv.create false
COPY pyproject.toml poetry.lock ./
RUN poetry install
COPY app app
CMD exec uvicorn --port=${PORT} app.main:app
