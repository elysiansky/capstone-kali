# Use the official Kali Linux base image
FROM kalilinux/kali-rolling

# Update and install basic packages
RUN apt-get update && apt-get install -y \
    net-tools \
    iputils-ping \
    vim \
    curl \
    wget \
    git \
    openssh-server \
    apache2

# Set up a non-root user
RUN useradd -m kaliuser && echo "kaliuser:kali" | chpasswd && adduser kaliuser sudo

# Create SSH directory and set permissions
RUN mkdir /home/kaliuser/.ssh && chown kaliuser:kaliuser /home/kaliuser/.ssh

# Configure SSH to allow password authentication
RUN sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config

# Expose necessary ports
EXPOSE 22 80

# Start SSH and Apache in the foreground
CMD service ssh start && apachectl -D FOREGROUND
