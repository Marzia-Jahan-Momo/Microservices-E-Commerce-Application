FROM python:3.12.4-slim as base

FROM base as builder

COPY requirements.txt .

RUN pip install --prefix="/install" -r requirements.txt


# Final stage
FROM base

WORKDIR /loadgen

COPY --from=builder /install /usr/local

# Add application code.
COPY locustfile.py .

# enable gevent support in debugger
ENV GEVENT_SUPPORT=True

ENTRYPOINT locust --host="http://${FRONTEND_ADDR}" --headless -u "${USERS:-10}" 2>&1
