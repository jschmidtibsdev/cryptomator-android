FROM debian:bookworm

RUN apt-get update -y && apt-get install -y --no-install-recommends \
    apt-utils wget git unzip openjdk-17-jdk ca-certificates \
    && rm -rf /var/lib/apt/lists/*

ENV ANDROID_COMMAND_LINE_TOOLS_FILENAME=commandlinetools-linux-10406996_latest.zip
ENV ANDROID_API_LEVELS=android-35
ENV ANDROID_BUILD_TOOLS_VERSION=35.0.1
ENV ANDROID_HOME=/usr/local/android-sdk-linux
ENV PATH=${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools:${ANDROID_HOME}/cmdline-tools/bin

RUN wget -q "https://dl.google.com/android/repository/${ANDROID_COMMAND_LINE_TOOLS_FILENAME}" \
    && unzip ${ANDROID_COMMAND_LINE_TOOLS_FILENAME} -d ${ANDROID_HOME} \
    && rm ${ANDROID_COMMAND_LINE_TOOLS_FILENAME}

RUN yes | sdkmanager --update --sdk_root="${ANDROID_HOME}"
RUN yes | sdkmanager --sdk_root="${ANDROID_HOME}" "platforms;${ANDROID_API_LEVELS}" "build-tools;${ANDROID_BUILD_TOOLS_VERSION}"
RUN yes | sdkmanager --licenses --sdk_root="${ANDROID_HOME}"

RUN rm -rf ${ANDROID_HOME}/tools

RUN groupadd -r appuser && useradd --no-log-init -r -g appuser appuser
USER appuser
