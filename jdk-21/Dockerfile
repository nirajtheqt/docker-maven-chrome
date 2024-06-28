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
# Download and install ChromeDriver
ENV CHROMEDRIVER_VERSION=126.0.6478.126
RUN wget -q -O '/tmp/chromedriver.zip https://storage.googleapis.com/chrome-for-testing-public/$CHROME_DRIVER_VERSION/linux64/chromedriver-linux64.zip' \
	&& unzip /tmp/chromedriver.zip -d /opt \
	&& rm /tmp/chromedriver.zip \
	&& ln -s /opt/chromedriver-linux64/chromedriver /usr/bin/chromedriver
# Set display port to avoid crash
# ENV DISPLAY=:99

# Verify installations
RUN google-chrome --version \
    && chromedriver --version

# Your commands and settings for your application
# COPY . /your-app
# WORKDIR /your-app
# RUN mvn clean install

# CMD ["mvn", "test"]
