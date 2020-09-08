# Using official python runtime base image
FROM python:2.7-alpine

ARG user=siva
ARG group=siva
ARG uid=1000
ARG gid=1000

# Set the application directory
WORKDIR /app



# Install our requirements.txt
ADD requirements.txt /app/requirements.txt
RUN pip install -r requirements.txt

RUN addgroup -g ${gid} ${group} \
    && adduser -u ${uid} -G ${group} -s /bin/sh -D ${user} \
    && chown -R ${user}:${group} /app 

# Copy our code from the current folder to /app inside the container
ADD . /app

# As we are creating for non-root making sure the port is also non privilized
EXPOSE 8080

USER ${user}

# Define our command to be run when launching the container
CMD ["gunicorn", "siva:siva", "-b", "0.0.0.0:8080", "--log-file", "-", "--access-logfile", "-", "--workers", "4", "--keep-alive", "0"]
