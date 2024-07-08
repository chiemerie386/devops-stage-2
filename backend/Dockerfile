# Use an official Python runtime as a parent image
FROM python:3.10-slim
# Set the working directory

# Install PostgreSQL client tools
RUN apt-get update && apt-get install -y postgresql-client

WORKDIR /app
# Install Poetry
RUN pip install poetry
# Copy the pyproject.toml and poetry.lock files
COPY pyproject.toml poetry.lock ./
# Install dependencies
RUN poetry install --no-root --no-dev
# Copy the rest of the application code
COPY . .
# Expose port 8000
EXPOSE 8000
ENV PYTHONPATH=/app
# Start app
RUN poetry run bash ./prestart.sh
# Command to run the FastAPI server
CMD ["poetry", "run", "uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]