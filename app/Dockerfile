# Use a lightweight python image to reduce attack surface area
FROM python:3.11-slim

WORKDIR /app

# Install dependencies first to leverage Docker layer caching
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application code
COPY app.py .

# Run as a non-root user for security best practices
RUN useradd -u 8888 appuser && chown -R appuser:appuser /app
USER appuser

EXPOSE 5000

# Use Gunicorn as a production-grade WSGI server
CMD ["gunicorn", "--bind", "0.0.0.0:5000", "app:app"]

