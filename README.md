# th2 gRPC check2-recon library

This library contains proto messages and `Check2Recon` service with RPC methods that are used
in [th2-check2-recon](https://github.com/th2-net/th2-check2-recon "th2-check2-recon").
See [check2-recon.proto](src/main/proto/th2_grpc_check2_recon/check2_recon.proto "check2_recon.proto") file for
details. <br>
Tool generates code from `.proto` files and uploads built packages (`.proto` files and generated code) to the specified
repositories.

## How to maintain project

1. Make your changes.
2. Up version of Java package in `gradle.properties` file.
3. Up version of Python package in `package_info.json` file.
4. Commit everything.

## How to run project

### Java
If you wish to manually create and publish a package for Java, run the following command:
```
gradle --no-daemon clean build publish artifactoryPublish \
       -Purl=${URL} \ 
       -Puser=${USER} \
       -Ppassword=${PASSWORD}
```
`URL`, `USER` and `PASSWORD` are parameters for publishing.

### Python
If you wish to manually create and publish a package for Python:
1. Generate services with `Gradle`:
    ```
       gradle --no-daemon clean generateProto
    ```
   You can find the generated files by following path: `src/gen/main/services/python`
2. Generate code from `.proto` files and publish everything using `twine`:
    ```
    pip install -r requirements.txt
    pip install twine
    python setup.py generate
    python setup.py sdist
    twine upload --repository-url ${PYPI_REPOSITORY_URL} --username ${PYPI_USER} --password ${PYPI_PASSWORD} dist/*
    ```
    `PYPI_REPOSITORY_URL`, `PYPI_USER` and `PYPI_PASSWORD` are parameters for publishing.