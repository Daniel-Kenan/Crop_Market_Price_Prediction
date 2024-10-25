# Use the official Python image from the Docker Hub
FROM python:3.11-slim

# Set the working directory in the container
WORKDIR /app

# Copy the requirements file into the container
COPY Crop_Production/requirements.txt .

# Install the dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy the entire Crop_Production directory into the container
COPY Crop_Production/ .

# Expose the port that the Flask app runs on
EXPOSE 5000

# Set the environment variable for Flask
ENV FLASK_APP=app.py

# Run the Flask application
CMD ["gunicorn", "--bind", "0.0.0.0:5000", "app:app"]

