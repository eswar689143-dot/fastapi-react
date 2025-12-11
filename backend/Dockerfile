# 1) Build Stage (optional for Python dependencies)
FROM python:3.11-slim AS builder

# set workdir
WORKDIR /app

# Install build dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# Copy dependency files
COPY requirements.txt .


# Install dependencies into a layer
RUN pip install --upgrade pip
RUN pip install --prefix=/install -r requirements.txt

# ----------------------------------------

# 2) Final Runtime Stage
FROM python:3.11-slim

WORKDIR /app

# Copy installed packages from builder
COPY --from=builder /install /usr/local

# Copy application code
COPY . .

# Expose FastAPI default port
EXPOSE 8000

# Run via uvicorn
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
