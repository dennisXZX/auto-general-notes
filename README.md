## Auto & General notes

__Not getting the latest package due to Intellij gradle cache__

- clear the gradle cache `rm -rf $HOME/.gradle/caches/`

- refresh gradle dependencies

__Run motorcycle-service locally__

- update Nginx config file `nginx-int.conf` at `/usr/local/etc/nginx/servers`, so the motorcycle-service request (`http://localhost:8888/api/example-micro-service/1.0/`) can be handled by Nginx

- start Nginx `sudo nginx`

- clone the motorcycle-service repo from Bitbucket (for example, motorcycle-service)

- set the VM options in IntelliJ for the project

```
// for motorcycle-service
-Dspring.profiles.active=INT -DMASTER_PASSWORD=SomethingSomethingSomething
```

- change the port number in `motorcycle-service/src/main/resources/application.yml` to `8081` so it doesn't conflict with other locally run micro service (for example, motorcycle-lookup-service)

- build the service `./gradlew clean build` (you can skip tests by `./gradlew clean build -x test`). You need to install gradle first `brew install gradle` if you don't have it on your machine

- run the application in IntelliJ

- visit `http://localhost:9000/?apiHost=http://localhost:8888`

In order to build with tests successfully, you would need to set the required envionment variables

```
# set the env variable
export MASTER_PASSWORD=3dYgu2rkMqobqsILnZJCTZpP

# build with DMASTER_PASSWORD
./gradlew -DMASTER_PASSWORD=3dYgu2rkMqobqsILnZJCTZpP clean build

# build with test skipped
./gradlew clean build -x jacocoTestCoverageVerification
./gradlew clean build -x test
```

You can use the `publishToMavenLocal` option to build a package to Maven local to address version number conflicts.

```
./gradlew clean build pTML
```

__Ngnix common commands__

- start Nginx `sudo nginx`
- reload Nginx `sudo nginx -s reload`
- stop Nginx `sudo nginx -s stop`

__Intercept CSAPI2 token__

- Set a break point in `CsApi2AccessTokenRequestInterceptor.java`

