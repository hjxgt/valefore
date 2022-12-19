FROM golang

WORKDIR /app

ADD go.mod .
ADD go.sum .
ADD main.go .

RUN go build -o main main.go

# copy to the next place
FROM alpine:3.17

WORKDIR /app

COPY --from=builder /app/main main
COPY public public
COPY templates templates

ENV PORT=3000

HEALTHCHECK --interval=30s --timeout=30s --start-period=5s --retries=3 CMD curl http://localhost:${PORT}/healthz || exit 1

EXPOSE ${PORT}

ENTRYPOINT ["app/main"]