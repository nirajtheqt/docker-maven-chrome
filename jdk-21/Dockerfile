FROM maven:3.9.6-eclipse-temurin-21
# Set the Chrome and ChromeDriver versions
# ENV CHROME_VERSION=126.0.6478.126
ENV CHROMEDRIVER_VERSION=126.0.6478.126

# Install dependencies
RUN apt-get update -qqy \
    && apt-get -qqy install gnupg2 wget unzip

# Download and install a specific version of Google Chrome
RUN wget -q https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
    && apt-get -qqy install ./google-chrome-stable_current_amd64.deb \
    && rm google-chrome-stable_current_amd64.deb \
    && rm -rf /var/lib/apt/lists/* /var/cache/apt/* \
    && sed -i 's|"$HERE/chrome"|"${HERE}/chrome" --no-sandbox|g' /opt/google/chrome/google-chrome

# Add ChromeDriver for the specific Chrome version
RUN wget -q "https://chromedriver.storage.googleapis.com/${CHROMEDRIVER_VERSION}/chromedriver_linux64.zip" \
    && unzip chromedriver_linux64.zip \
    && rm chromedriver_linux64.zip \
    && mv chromedriver /usr/local/bin/chromedriver \
    && chmod +x /usr/local/bin/chromedriver
# Verify installations
RUN google-chrome --version \
    && chromedriver --version
