# Use Ubuntu Jammy (22.04) as the base image
FROM ubuntu:22.04

# Expose the port your application will run on
EXPOSE 8080

# Update and install Python, pip, and adduser
RUN apt update && apt install -y \
    python3 \
    python3-pip \
    adduser

# Set the working directory
WORKDIR /home/julius/llm

# Create a non-root user and assign permissions
RUN adduser -u 5678 --disabled-password --gecos "" julius && \
    chown -R julius /home/julius/llm

# Switch to the new non-root user
USER julius

# Install Gunicorn and Uvicorn
RUN pip install --no-cache-dir gunicorn uvicorn

# Run your FastAPI app with Gunicorn
CMD ["gunicorn", "--bind", "0.0.0.0:8080", "-k", "uvicorn.workers.UvicornWorker", "myapp.app:app"]
