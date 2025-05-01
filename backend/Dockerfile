FROM python:3.11-bookworm

RUN apt-get update && apt-get install -y \
    python3-dev \
    libjpeg-dev \
    zlib1g-dev \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app
COPY requirements.txt .

RUN pip install --upgrade pip && \
    pip install wheel && \
    pip install --no-cache-dir --no-deps Pillow==9.0.0 && \
    pip install --no-cache-dir --no-deps psycopg2-binary==2.9.3 && \
    pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["gunicorn", "--bind", "0.0.0.0:9000", "kittygram_backend.wsgi"]
