# totally naming this rfdocker 2.0 ;p

ARG PYTHON_VERSION=3.7.4
FROM python:${PYTHON_VERSION}-alpine

# pass tzdata as ADD_APK_PACKAGE for testing on these timezones rather than UTC
ARG ADD_APK_PACKAGES=""
RUN apk add --no-cache ${ADD_APK_PACKAGES} && \
    rm -rf /var/cache/* /tmp/* /var/log/* ~/.cache

# ...and set is as following
#RUN cp /usr/share/zoneinfo/Europe/Helsinki /etc/localtime
#RUN echo "Europe/Helsinki" > /etc/timezone

ARG UNAME="robot"
ARG HOST_UID=1000
ARG SHELL="/bin/sh"
RUN adduser -D ${UNAME} -u ${HOST_UID} -s ${SHELL}

USER ${UNAME}
WORKDIR /home/${UNAME}

ENV PATH=/home/${UNAME}/.local/bin:$PATH
ARG ADD_PY_PACKAGES="robotframework==3.1.2"
RUN pip install --no-cache-dir --user ${ADD_PY_PACKAGES}

COPY --chown=robot:robot requirements.txt .
RUN pip install --no-cache-dir --user -r requirements.txt

ENV PYTHONPATH=/home/${UNAME}/src
COPY --chown=robot:robot src src

ENTRYPOINT ["python", "-m"]
