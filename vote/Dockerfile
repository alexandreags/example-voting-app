# Using official python runtime base image
FROM python:3.11

# add curl for healthcheck
#RUN sed -i s/deb.debian.org/archive.debian.org/g /etc/apt/sources.list.d/debian.sources 
#RUN sed -i 's|security.debian.org|archive.debian.org/debian-security/|g' /etc/apt/sources.list.d/debian.sources 
#RUN sed -i '/stretch-updates/d' /etc/apt/sources.list.d/debian.sources
RUN apt-get update 
RUN apt-get install -y --no-install-recommends curl 
RUN rm -rf /var/lib/apt/lists/*

# Set the application directory
WORKDIR /app

# Install our requirements.txt
COPY requirements.txt /app/requirements.txt
RUN pip install -r requirements.txt

# Copy our code from the current folder to /app inside the container
COPY . .

# Make port 5000 available for links and/or publish
EXPOSE 5000

# Define our command to be run when launching the container
CMD ["gunicorn", "app:app", "-b", "0.0.0.0:80", "--log-file", "-", "--access-logfile", "-", "--workers", "4", "--keep-alive", "0"]
