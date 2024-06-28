FROM maven:eclipse-temurin

ENV CHROME_VERSION=126.0.6478.126
ENV CHROMEDRIVER_VERSION=126.0.6478.126

# Install dependencies
RUN apt-get update -qqy \
    && apt-get -qqy install gnupg2 wget unzip xvfb \
    # Install additional dependencies required by Chrome
    && apt-get -qqy install libgconf-2-4 libnss3 libxss1 libasound2 libatk-bridge2.0-0 libgtk-3-0

# Create directory for Chrome installation
RUN mkdir -p /opt/google/chrome

# Download and install Chrome
RUN wget -q "https://storage.googleapis.com/chrome-for-testing-public/$CHROME_VERSION/linux64/chrome-linux64.zip" \
    && unzip chrome-linux64.zip -d /opt/google/chrome \
    && rm chrome-linux64.zip \
    && ln -s /opt/google/chrome/chrome-linux64/chrome /usr/bin/google-chrome \
    && chmod +x /opt/google/chrome/chrome-linux64/chrome \
    && google-chrome --version

# Download and install ChromeDriver
RUN wget -q "https://chromedriver.storage.googleapis.com/${CHROMEDRIVER_VERSION}/chromedriver_linux64.zip" \
    && unzip chromedriver_linux64.zip \
    && mv chromedriver /usr/local/bin/chromedriver \
    && rm chromedriver_linux64.zip \
    && chmod +x /usr/local/bin/chromedriver \
    && chromedriver --version

# Default command
CMD ["tail", "-f", "/dev/null"]
