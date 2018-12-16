FROM python:2.7.15

RUN pip install troposphere \
                awacs \
                pyyaml \
                yapf==0.11.0 \
                flake8 \
                autoflake \
                codeclimate-test-reporter \
                rainbow_logging_handler

RUN mkdir -p /usr/src/app

COPY artifacts/hello.py /usr/src/app

WORKDIR /usr/src/app
RUN chmod 777 hello.py
ENTRYPOINT ["python", "/usr/src/app/hello.py"]