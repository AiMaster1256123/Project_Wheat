FROM python:3.13-slim AS validator
WORKDIR /validate
RUN pip install --no-cache-dir pyyaml
COPY litellm_config.yaml ./
RUN python -c "import yaml,sys; yaml.safe_load(open('litellm_config.yaml')); print('ok')"

FROM ghcr.io/berriai/litellm:v1.83.3-stable
COPY --from=validator /validate/litellm_config.yaml /app/config.yaml
RUN id litellm 2>/dev/null || useradd --system --no-create-home --uid 1001 litellm
USER litellm
EXPOSE 4000
HEALTHCHECK --interval=30s --timeout=10s --start-period=20s --retries=3 \
  CMD python -c "import urllib.request,sys; urllib.request.urlopen('http://localhost:4000/health/liveliness') or sys.exit(1)"
ENTRYPOINT ["litellm"]
CMD ["--config", "/app/config.yaml", "--port", "4000"]
