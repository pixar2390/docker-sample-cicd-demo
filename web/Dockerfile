FROM node:18 AS base
CMD [ "bash" ]

# Build
FROM base AS test-and-build
COPY . /workspace
WORKDIR /workspace
ARG REACT_APP_API_SERVER
RUN npm ci && npm run test && npm run build

# Hosting in nginx
FROM nginx:latest AS production
# --from=test-and-buildとしているのでtest-and-buildと名前をつけたステージも実行されて、必要なファイルをコピーする。ただ、最後に提供されるのはtargetで指定したステージ情報だけ
COPY --from=test-and-build /workspace/build /var/www
COPY nginx.conf /etc/nginx/conf.d/default.conf
