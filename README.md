# Docker container for Watir/Capybara tests against a local Chrome

Includes:

* Chromedriver (2.27)
* Google Chrome (latest at build-time)
* Ruby (2.3.1)

Based off the `ruby:2.3.1` and `github.com/robcherry/docker-chromedriver`
container. This is not a small container (by any margin); it's for
convenience in development (and light CI usage).

# Building

```
docker build github.com/levlozhkin/ruby-chromedriver
```

# Example usage

```
docker run -t ruby-chromedriver:1.0.0 -v .:/watir -v ~/.bundle:/bundle
    -e BUNDLE_PATH=/bundle --shm-size=1024m -- run.sh
```

`Run.sh` contents:

```
#!/bin/sh

set -ex

if ! bundle check; then
    bundle install --jobs 4 --retry 5
fi

bundle exec cucumber
```
