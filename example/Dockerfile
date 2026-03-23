FROM python:3.10-slim

WORKDIR /app

# Install system dependencies if needed (e.g., for IRIS python client if it needs them)
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# Copy the source code of the MCP server
COPY src/ /app/src/
COPY pyproject.toml /app/

# Install the MCP server package
RUN pip install --no-cache-dir .

# Copy the example client
COPY example/mcp.py /app/example/mcp.py
COPY example/requirements-dev.txt /app/example/requirements-dev.txt

# Install example dependencies
RUN pip install --no-cache-dir -r /app/example/requirements-dev.txt

# Set environment variables for the example
ENV IRIS_HOSTNAME=iris
ENV IRIS_PORT=1972
ENV IRIS_NAMESPACE=USER
ENV IRIS_USERNAME=_SYSTEM
ENV IRIS_PASSWORD=SYS

WORKDIR /app/example

CMD ["python", "mcp.py"]
