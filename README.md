# uaa

This application was generated using JHipster 6.0.1, you can find documentation and help at [https://www.jhipster.tech/documentation-archive/v6.0.1](https://www.jhipster.tech/documentation-archive/v6.0.1).

This is a "uaa" application intended to be part of a microservice architecture, please refer to the [Doing microservices with JHipster][] page of the documentation for more information.

This is also a JHipster User Account and Authentication (UAA) Server, refer to [Using UAA for Microservice Security][] for details on how to secure JHipster microservices with OAuth2.
This application is configured for Service Discovery and Configuration with the JHipster-Registry. On launch, it will refuse to start if it is not able to connect to the JHipster-Registry at [http://localhost:8761](http://localhost:8761). For more information, read our documentation on [Service Discovery and Configuration with the JHipster-Registry][].

## Support for Authorization Code Flow

Use browser to access the below url to simulate an oath client with client id `sampleClientId` and redirect uri `http://localhost:8080/ui/login` and the scope `openid`

    http://localhost:9999/oauth/authorize?response_type=code&client_id=alexa&redirect_uri=http://localhost:8080/ui/login&scope=openid&state=1234


A custom login page is hosted at `/login` which you will be forwarded to after accessing the above url.

The default login credentials username=admin and password=admin can be used to login.

After login, the browser is forwarded to the redirect uri with the auth code. The url would for example look as shown below.

`http://localhost:8080/ui/login?code=V5A7lB&state=1234`

To use the auth code, the server hosting the oauth client would then perform the following POST request

    curl -u alexa:secret http://localhost:9999/oauth/token -d code=V5A7lB -d grant_type=authorization_code -d client_id=alexa -d client_secret=secret -d redirect_uri=http://localhost:8080/ui/login

This will return a response like the one below

```json
{
  "access_token" : "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyX25hbWUiOiJhZG1pbiIsInNjb3BlIjpbIm9wZW5pZCJdLCJleHAiOjE1NjEyNjUzMDUsImlhdCI6MTU2MTIyMjEwNSwiYXV0aG9yaXRpZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJqdGkiOiJmY2I4ZDg1Yi00NmFiLTQ3N2MtYmQzNS1mNTBhZWZjODlhZDAiLCJjbGllbnRfaWQiOiJhbGV4YSJ9.IWIW0-pwhJoguQFc6wo61HyzjUFOXPJMsu2NsXwQWo05xx3CbfTgAddRKcDBBcbdVhu2peKMiaszdGqRPHjBcyrbJdyFBH4W3SktZ-ETn7Q6brfbEtSMSbQ10jEJ4ECRtMZaUe-PH8OOkbzd1cKnzl5qnudH5e6nXUWJah0tKaSVI6c1l_NJNEgMZjqDYRdajTzFtNYsoV40xRAn1QKCsVe7V7lrmTR74t8pGLF2WLUyg6kAQdo7Q1YvaFmqp7QqN-yC0c_A-mjzS3VvASu6koKZRz6sbiJFuT3CZRy7l8Zffn_2cPXqccPvdYlZnlLsfDUihepU2c640KxfjmgTOA",
  "token_type" : "bearer",
  "expires_in" : 43199,
  "scope" : "openid",
  "iat" : 1561222105,
  "jti" : "fcb8d85b-46ab-477c-bd35-f50aefc89ad0"
}
```

The decoded token has the following information

```json
{
  "user_name": "admin",
  "scope": [
    "openid"
  ],
  "exp": 1561265305,
  "iat": 1561222105,
  "authorities": [
    "ROLE_ADMIN",
    "ROLE_USER"
  ],
  "jti": "fcb8d85b-46ab-477c-bd35-f50aefc89ad0",
  "client_id": "alexa"
}
```

## Development

To start your application in the dev profile, simply run:

    ./gradlew

For further instructions on how to develop with JHipster, have a look at [Using JHipster in development][].

## Building for production

### Packaging as jar

To build the final jar and optimize the uaa application for production, run:

    ./gradlew -Pprod clean bootJar

To ensure everything worked, run:

    java -jar build/libs/*.jar

Refer to [Using JHipster in production][] for more details.

### Packaging as war

To package your application as a war in order to deploy it to an application server, run:

    ./gradlew -Pprod clean bootWar

## Testing

To launch your application's tests, run:

    ./gradlew test integrationTest

For more information, refer to the [Running tests page][].

### Code quality

Sonar is used to analyse code quality. You can start a local Sonar server (accessible on http://localhost:9001) with:

```
docker-compose -f src/main/docker/sonar.yml up -d
```

You can run a Sonar analysis with using the [sonar-scanner](https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner) or by using the gradle plugin.

Then, run a Sonar analysis:

```
./gradlew -Pprod clean check sonarqube
```

For more information, refer to the [Code quality page][].

## Using Docker to simplify development (optional)

You can use Docker to improve your JHipster development experience. A number of docker-compose configuration are available in the [src/main/docker](src/main/docker) folder to launch required third party services.

For example, to start a mysql database in a docker container, run:

    docker-compose -f src/main/docker/mysql.yml up -d

To stop it and remove the container, run:

    docker-compose -f src/main/docker/mysql.yml down

You can also fully dockerize your application and all the services that it depends on.
To achieve this, first build a docker image of your app by running:

    ./gradlew bootJar -Pprod jibDockerBuild

Then run:

    docker-compose -f src/main/docker/app.yml up -d

For more information refer to [Using Docker and Docker-Compose][], this page also contains information on the docker-compose sub-generator (`jhipster docker-compose`), which is able to generate docker configurations for one or several JHipster applications.

## Continuous Integration (optional)

To configure CI for your project, run the ci-cd sub-generator (`jhipster ci-cd`), this will let you generate configuration files for a number of Continuous Integration systems. Consult the [Setting up Continuous Integration][] page for more information.

[jhipster homepage and latest documentation]: https://www.jhipster.tech
[jhipster 6.0.1 archive]: https://www.jhipster.tech/documentation-archive/v6.0.1
[doing microservices with jhipster]: https://www.jhipster.tech/documentation-archive/v6.0.1/microservices-architecture/

[Using UAA for Microservice Security]: https://www.jhipster.tech/documentation-archive/v6.0.1/using-uaa/[Using JHipster in development]: https://www.jhipster.tech/documentation-archive/v6.0.1/development/
[Service Discovery and Configuration with the JHipster-Registry]: https://www.jhipster.tech/documentation-archive/v6.0.1/microservices-architecture/#jhipster-registry
[Using Docker and Docker-Compose]: https://www.jhipster.tech/documentation-archive/v6.0.1/docker-compose
[Using JHipster in production]: https://www.jhipster.tech/documentation-archive/v6.0.1/production/
[Running tests page]: https://www.jhipster.tech/documentation-archive/v6.0.1/running-tests/
[Code quality page]: https://www.jhipster.tech/documentation-archive/v6.0.1/code-quality/
[Setting up Continuous Integration]: https://www.jhipster.tech/documentation-archive/v6.0.1/setting-up-ci/
