# Use Amazon Linux 2 base image
FROM amazonlinux:2

# Set working directory
WORKDIR /app

# Copy project files
COPY . /app

# Update and install dependencies
RUN yum update -y && \
    yum install -y python3 python3-pip mariadb105 && \
    yum clean all

# Install Python dependencies
RUN pip3 install --no-cache-dir -r requirements.txt

# Expose Flask port
EXPOSE 5000

# Start Flask backend app
CMD ["python3", "rds.py"]
