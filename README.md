# AWS Serverless Application Model fo ASP.Net Core Apps
![CircleCI](https://img.shields.io/circleci/build/github/sevensc/typescript-string-operations?logo=circleci&token=e3f75ec3d21d6da12384faf594c9d05fe9f65747)
[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=iwt-alexanderpuscher_aws-poc-estate-cloud-contacts-service&metric=alert_status)](https://sonarcloud.io/dashboard?id=iwt-alexanderpuscher_aws-poc-estate-cloud-contacts-service)

https://medium.com/@ravi.aakula/aws-serverless-application-model-for-asp-net-core-apps-1ce03e0e389d

## Prerequisite

CircleCI CLI
```
choco install circleci-cli
```


## Setup

### Install AWS lambda and serverless templates

```
dotnet new -i Amazon.Lambda.Templates
```

### Creating the API

Create a new folder you want your code to reside in and run:

```
dotnet new serverless.AspNetCoreWebAPI --name estate-cloud-contacts-service
cd estate-cloud-contacts-service\src\estate-cloud-contacts-service
dotnet restore
dotnet run
```

### Add swagger support

```
dotnet add package Swashbuckle.AspNetCore
```

### Register the Swagger generator in Configure services place.

```
services.AddSwaggerGen(c =>{
    c.SwaggerDoc("v1", new OpenApiInfo { Title = "AWS Serverless Asp.Net Core Web API", Version = "v1" });
});
```

### Enable swagger middleware and use swagger UI .

```
app.UseSwagger();
app.UseSwaggerUI(c =>
{
    c.SwaggerEndpoint("v1/swagger.json", "AWS Serverless Asp.Net Core Web API");
    c.RoutePrefix = "swagger";
});
```

### Install lambda tools to publish this application to AWS

```
dotnet tool install -g Amazon.Lambda.Tools
```

### Create a S3 bucket in AWS console to upload source code packages and build outputs.

### Create an IAM user and download creadentials to local machine and configure AWS profile in your local machine.

### Now publish this application to AWS as serverless model.

```
dotnet lambda deploy-serverless --stackname estate-cloud-contacts-service --profile personal --region eu-central-1 --s3-bucket estate-cloud-contacts-service-builds
```

### Copy URL from output and browse swagger route. You should be able to see the swagger UI.

## Development

### Validate A CircleCI Config

```
circleci config validate
```

### Processing A Config

```
circleci config process .circleci/config.yml >> .circleci/config_compiled.yml
```
