# Use an official Python base image
FROM python:3.14.0a5-bookworm

# Set the working directory inside the container
WORKDIR /app

# Copy and install dependencies
COPY req.txt .
RUN pip install --no-cache-dir -r req.txt

# Copy Flask application code
COPY . .

# Expose the correct port
EXPOSE 8387

# Run the application
CMD ["python", "app.py"]
