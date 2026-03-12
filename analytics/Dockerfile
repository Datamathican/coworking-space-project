# Use a lightweight official Python base image to keep the image size small
FROM python:3.10-slim

# Set the working directory inside the container
WORKDIR /app

# Copy only the requirements file first to leverage Docker layer caching
COPY requirements.txt .

# Install dependencies without caching to minimize the final container image size
RUN pip install --no-cache-dir -r requirements.txt

# Copy the remaining application source code into the container
COPY . .

# Expose the port the Flask application listens on
EXPOSE 5153

# Start the application using the Python interpreter
CMD ["python", "app.py"]