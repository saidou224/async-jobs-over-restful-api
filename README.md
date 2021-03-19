# async-jobs-over-restful-api
Submit long running jobs for asynchronous processing over a RESTful API.

# Setup

## Clone the repository
```
$ git clone git@github.com:sanketdaru/async-jobs-over-restful-api.git
```

## Change to directory with cloned repository
```
$ cd async-jobs-over-restful-api
```

## Ensure you have JDK 11 or later installed and set as JAVA_HOME.
```
$ java -version
openjdk version "15.0.1" 2020-10-20
OpenJDK Runtime Environment Corretto-15.0.1.9.1 (build 15.0.1+9)
OpenJDK 64-Bit Server VM Corretto-15.0.1.9.1 (build 15.0.1+9, mixed mode, sharing)
```

# Run project

Using gradle-wrapper run the SpringBoot project
```
$ ./gradlew bootRun
```
or if you're on Windows
```
$ gradlew.bat bootRun
```

This will run the embedded Tomcat bound to `localhost` and listening on port `8080`

# Test

Use your favourite REST client to issue requests and check the output. For the simplistic use-case that it is, `curl` can also be used.

1. POST a new job submit a file named sample.txt for asynchronous processing
``` curl
curl --location --request POST 'http://localhost:8080/api/v1/jobs' \
--form 'file=@"sample.txt"'
```

2. GET the status of the posted asynchronous job. Use `job_id` received as response from posting a new job command as an input to next command
``` curl
curl --location --request GET 'http://localhost:8080/api/v1/jobs/{job_id}'
```

3. GET the output file produced as a result of completion of the posted asynchronous job. Use the `output_file_uri` received as response from get the status command as an input to next command
``` curl
curl --location --request GET 'http://localhost:8080/{output_file_uri}'
```

4. DELETE the job as well as the output file. Use `job_id` received as response from posting a new job command as an input to next command
``` curl
curl --location --request DELETE 'http://localhost:8080/api/v1/jobs/d0f69d7a-a8b9-422b-8f48-3789ae1309b2'
```
