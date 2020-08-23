FROM ruby:2.7.1-alpine

ENV RUNTIME_PACKAGES "linux-headers libxml2-dev make gcc libc-dev nodejs tzdata postgresql-dev postgresql imagemagick vim"
ENV DEV_PACKAGES "build-base curl-dev"
ENV APP_HOME /app
ENV TZ Asia/Tokyo
ENV LANG C.UTF-8

ENV HOST 0.0.0.0
ENV PORT 3000

WORKDIR ${APP_HOME}
ADD Gemfile ${APP_HOME}/Gemfile
ADD Gemfile.lock ${APP_HOME}/Gemfile.lock

RUN apk update \
  && apk upgrade \
  && apk add --update --no-cache ${RUNTIME_PACKAGES} \
  && apk add --update --no-cache --virtual=.build-dependencies ${DEV_PACKAGES} \
  && bundle install -j4 \
  && rm -rf /usr/local/bundle/cache/*.gem \
  && find /usr/local/bundle/gems/ -name "*.c" -delete \
  && find /usr/local/bundle/gems/ -name "*.o" -delete \
  && apk del --purge .build-dependencies \
  && rm -rf /var/cache/apk/*

COPY . ${APP_HOME}

EXPOSE ${PORT}

CMD ["rails", "server", "-b", ${HOST}]
