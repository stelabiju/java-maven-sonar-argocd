# Use a slim image for a smaller footprint
FROM python:3.12-slim

# Set environment variables to prevent Python from buffering stdout/stderr
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

WORKDIR /opt/app

# Install system dependencies (e.g., if you use PostgreSQL later)
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# Install python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt gunicorn

# Copy only necessary files
COPY . .

# Expose port
EXPOSE 8000

# Use Gunicorn to run the application (Point to your wsgi file)
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "test_django_pro.wsgi:application"]
