# Use official Ubuntu base image
FROM ubuntu:22.04

# Set environment variables to non-interactive
ENV DEBIAN_FRONTEND=noninteractive

# Update package list and install PostgreSQL
RUN apt-get update && \
    apt-get install -y postgresql postgresql-contrib && \
    apt-get clean

# Expose PostgreSQL default port
EXPOSE 5432

# Create a new PostgreSQL user and database
USER postgres
RUN /etc/init.d/postgresql start && \
    psql --command "CREATE USER myuser WITH SUPERUSER PASSWORD 'mypassword';" && \
    createdb -O myuser mydatabase

# Start PostgreSQL server
CMD ["/usr/lib/postgresql/14/bin/postgres", "-D", "/var/lib/postgresql/14/main", "-c", "config_file=/etc/postgresql/14/main/postgresql.conf"]

FROM alpine
CMD ["echo", "Hello from Docker!"]
