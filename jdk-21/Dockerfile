FROM maven:3.9.6-eclipse-temurin-21

# Install dependencies
RUN apt-get update -qqy \
    && apt-get -qqy install gnupg2 wget unzip

# Download and install Google Chrome
RUN wget -q https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
    && apt-get -qqy install ./google-chrome-stable_current_amd64.deb \
    && rm google-chrome-stable_current_amd64.deb \
    && rm -rf /var/lib/apt/lists/* /var/cache/apt/* \
    && sed -i 's|"$HERE/chrome"|"${HERE}/chrome" --no-sandbox|g' /opt/google/chrome/google-chrome

# Add ChromeDriver
ARG CHROMEDRIVER_VERSION=latest
RUN if [ "$CHROMEDRIVER_VERSION" = "latest" ]; then CHROMEDRIVER_VERSION=$(wget -qO- https://chromedriver.storage.googleapis.com/LATEST_RELEASE); fi \
    && wget -q "https://chromedriver.storage.googleapis.com/$CHROMEDRIVER_VERSION/chromedriver_linux64.zip" \
    && unzip chromedriver_linux64.zip \
    && rm chromedriver_linux64.zip \
    && mv chromedriver /usr/local/bin/chromedriver \
    && chmod +x /usr/local/bin/chromedriver

# Set display port to avoid crash
ENV DISPLAY=:99

# Verify installations
RUN google-chrome --version \
    && chromedriver --version

# Your commands and settings for your application
# COPY . /your-app
# WORKDIR /your-app
# RUN mvn clean install

# CMD ["mvn", "test"]
