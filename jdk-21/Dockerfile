FROM maven:3.9.6-eclipse-temurin-21
# Set the Chrome and ChromeDriver versions
ENV CHROME_VERSION=126.0.6478.126
ENV CHROMEDRIVER_VERSION=126.0.6478.126

# Install dependencies
RUN apt-get update -qqy \
    && apt-get -qqy install gnupg2 wget unzip

# Download and install Chrome
RUN wget -q "https://storage.googleapis.com/chrome-for-testing-public/${CHROME_VERSION}/linux64/chrome-linux64.zip" \
    && unzip chrome-linux64.zip \
    && mv chrome-linux64 /opt/google/chrome \
    && rm chrome-linux64.zip \
    && ln -s /opt/google/chrome/chrome /usr/bin/google-chrome

# Download and install Chrome headless shell (if needed)
RUN wget -q "https://storage.googleapis.com/chrome-for-testing-public/${CHROME_VERSION}/linux64/chrome-headless-shell-linux64.zip" \
    && unzip chrome-headless-shell-linux64.zip \
    && mv chrome-headless-shell-linux64 /opt/google/chrome \
    && rm chrome-headless-shell-linux64.zip \
    && ln -s /opt/google/chrome/chrome-headless-shell /usr/bin/google-chrome-headless

# Download and install ChromeDriver
RUN wget -q "https://chromedriver.storage.googleapis.com/${CHROMEDRIVER_VERSION}/chromedriver_linux64.zip" \
    && unzip chromedriver_linux64.zip \
    && mv chromedriver /usr/local/bin/chromedriver \
    && rm chromedriver_linux64.zip \
    && chmod +x /usr/local/bin/chromedriver
# Verify installations
RUN google-chrome --version \
    && chromedriver --version
