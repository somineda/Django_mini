FROM python:3.13-slim

ENV PYTHONUNBUFFERED=1

WORKDIR /app

RUN pip install uv

COPY ../pyproject.toml ../uv.lock* ./

RUN uv sync --frozen

COPY .. .

EXPOSE 8000

CMD ["uv", "run", "gunicorn", "core.wsgi:application", "--bind", "0.0.0.0:8000"]