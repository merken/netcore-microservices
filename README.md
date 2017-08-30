# netcore-microservices
A microservices delivery setup with netcore and angular

By [Maarten Merken](https://github.com/merken).

## Description
**netcore-microservices** is a infrastructure template project to quickly get started with a local CI/CD environment using Jenkins and Docker.
At the base, there's the build/Dockerfile, which will provision a Jenkins CI environment using the build/spawnerjob.xml configuration file.
This is a freestyle jenkins job, using the [DSL Job plugin](https://jenkinsci.github.io/job-dsl-plugin/) to declaratively create other jenkins jobs based on DSL syntax.

For this demonstration, three jobs are created.
- ngapp (front end application)
- productservice (aspnet core microservice)
- userservice (aspnet core microservice)

Each service defines a pipeline job, the pipeline is described in a Jenkinsfile in the project directory.

## Installation as-is

Build the jenkins image.

```console
docker build build/. -t ngappmicroservices:latest
```

Run the container.

```console
docker run -d -p 8080:8080 -v /var/run/docker.sock:/var/run/docker.sock --name ngappmicroservices ngappmicroservices:latest
```

Your local Jenkins CI environment should now be up and running on http://localhost:8080.

Build the spawnerjob project, you should see 3 new pipeline projects on the jenkins homepage.

Build each project (ngapp, userservice, productservice).
After all three are successfully built, there should be three docker containers running on your host.
- ngapp (front end application)
- productservice (aspnet core microservice)
- userservice (aspnet core microservice)

These should be accessible via these endpoints:
- ngapp http://localhost:5002
- productservice http://localhost:5000
- userservice http://localhost:5001

## Usage

Feel free to tailer this project as you like, you can add more jobs in the build/spawnerjob.xml, modify the Dockerfiles and Jenkinsfiles to suit your needs.
Once your docker containers are built, you can upload them to a repository and use them for testing, staging and even production.

## Authors

* Maarten Merken (https://github.com/merken)

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## License

MIT License

Copyright (c) 2017 Maarten Merken

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.