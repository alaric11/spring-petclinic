FROM eclipse-temurin:21.0.1_12-jre

ARG USERNAME=app
ARG USER_UID=999
ARG USER_GID=$USER_UID

# Create the user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    #
    # [Optional] Add sudo support. Omit if you don't need to install software after connecting.
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

RUN mkdir /opt/app
COPY target/spring-petclinic-3.2.0-SNAPSHOT.jar /opt/app/app.jar
RUN chown -R app:app /opt/app

USER app

ENTRYPOINT ["/opt/java/openjdk/bin/java", "-Dspring.profiles.active=postgres", "-jar", "/opt/app/app.jar"]
