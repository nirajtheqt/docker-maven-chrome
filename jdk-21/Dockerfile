# Use Maven with JDK 21 base image
FROM maven:3.9.6-eclipse-temurin-21

# Set environment variables for ChromeDriver version
ENV CHROME_DRIVER_VERSION=128.0.6613.137

# Install dependencies
RUN apt-get update -qqy \
    && apt-get -qqy install wget unzip curl gnupg2 libnss3 libgconf-2-4 libxi6 libgbm1 libxrandr2 libxss1 libasound2 libatk-bridge2.0-0 libgtk-3-0 \
    && rm -rf /var/lib/apt/lists/* /var/cache/apt/*

# Download and install Chrome (new link)
RUN wget -q -O /tmp/chrome-linux64.zip "https://storage.googleapis.com/chrome-for-testing-public/${CHROME_DRIVER_VERSION}/linux64/chrome-linux64.zip" \
    && unzip /tmp/chrome-linux64.zip -d /opt/google/chrome/ \
    && rm /tmp/chrome-linux64.zip \
    && ln -s /opt/google/chrome/chrome /usr/bin/google-chrome

# Download and install ChromeDriver
RUN wget -q -O /tmp/chromedriver.zip "https://storage.googleapis.com/chrome-for-testing-public/${CHROME_DRIVER_VERSION}/linux64/chromedriver-linux64.zip" \
    && unzip /tmp/chromedriver.zip -d /opt \
    && rm /tmp/chromedriver.zip \
    && ln -s /opt/chromedriver-linux64/chromedriver /usr/bin/chromedriver \
    && chromedriver --version
