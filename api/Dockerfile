FROM gradle:7 AS base
CMD ["bash"]

# build
FROM base AS test-and-build
COPY . /workspace
WORKDIR /workspace
RUN ./gradlew build

# production
FROM openjdk:17 AS production
# --from=test-and-buildとしているのでtest-and-buildと名前をつけたステージも実行されて、必要なファイルをコピーする。ただ、最後に提供されるのはtargetで指定したステージ情報だけ
COPY --from=test-and-build /workspace/build/libs/api-0.0.1-SNAPSHOT.jar ./api.jar
CMD [ "java", "-jar", "api.jar" ]
