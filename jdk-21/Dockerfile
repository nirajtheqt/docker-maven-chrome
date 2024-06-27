FROM maven:3.9.6-eclipse-temurin-21

# Google Chrome

ARG CHROME_VERSION=126.0.6478.126
RUN apt-get update -qqy \
    && apt-get -qqy install gnupg2 wget unzip \
    && wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && echo "deb http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list \
    && apt-get update -qqy \
    && apt-get -qqy install google-chrome-stable=$CHROME_VERSION \
    && rm /etc/apt/sources.list.d/google-chrome.list \
    && rm -rf /var/lib/apt/lists/* /var/cache/apt/* \
    && sed -i 's|"$HERE/chrome"|"${HERE}/chrome" --no-sandbox|g' /opt/google/chrome/google-chrome

# ChromeDriver

ARG CHROME_DRIVER_VERSION=126.0.6478.126
RUN if [ "$CHROMEDRIVER_VERSION" = "latest" ]; then CHROMEDRIVER_VERSION=$(wget -qO- https://chromedriver.storage.googleapis.com/LATEST_RELEASE); fi \
    && wget -q "https://chromedriver.storage.googleapis.com/$CHROMEDRIVER_VERSION/chromedriver_linux64.zip" \
    && unzip chromedriver_linux64.zip \
    && rm chromedriver_linux64.zip \
    && mv chromedriver /usr/local/bin/chromedriver \
    && chmod +x /usr/local/bin/chromedriver
# Verify installations
RUN google-chrome --version \
    && chromedriver --version
