#springboot-s2i
FROM maven:3.6-ibmjava-8

# TODO: Put the maintainer name in the image metadata
LABEL maintainer="huabing.li"

# TODO: Rename the builder environment variable to inform users about application you provide them
ENV MAVEN_CONFIG=.m2

# TODO: Set labels used in OpenShift to describe the builder image
LABEL io.openshift.s2i.scripts-url="image:///usr/libexec/s2i" \
      io.openshift.s2i.assemble-user="1001" \
      io.openshift.s2i.destination="/opt/s2i/destination"

#LABEL io.k8s.description="Platform for building xyz" \
#      io.k8s.display-name="builder x.y.z" \
#      io.openshift.expose-services="8080:http" \
#      io.openshift.tags="builder,x.y.z,etc."

# TODO: Install required packages here:
WORKDIR /opt

RUN useradd -m deploy -u 1001 && \
    chmod -R 777 /opt && \
    mkdir -p /opt/s2i/destination && \
    chmod -R 777 /opt/s2i/destination

# TODO: Copy the S2I scripts to /usr/libexec/s2i, since openshift/base-centos7 image
# sets io.openshift.s2i.scripts-url label that way, or update that label
COPY ./s2i/bin/ /usr/libexec/s2i

# TODO: Drop the root user and make the content of /opt/app-root owned by user 1001
RUN chown -R 1001:1001 /opt && \
    chown -R 1001:1001 /var/ && \
    chmod -R a+rwx /opt

# This default user is created in the openshift/base-centos7 image
USER 1001

# TODO: Set the default port for applications built using this image
# EXPOSE 8080

# TODO: Set the default CMD for the image
# CMD ["/usr/libexec/s2i/usage"]
