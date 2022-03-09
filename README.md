# CIBR/FLARE Lake Forecast Automatic Deployment
This repository holds JSON configuration files for automated deployment of  multiple lake forecasts for the CIBR/FLARE project using OpenWhisk for microservice execution and S3 buckets to store and serve data.

The workflow for corecast users to have a lake forecast automatically deployed is as follows:

## Clone, develop, and test your own code repository
The first requirement is for a user to have a stable, tested code repository with the FLARE codebase applied to your lake. [Here is an example of the repository for FCR](https://github.com/FLARE-forecast/FCRE-forecast-code). 

Please follow the forecast code repository documentation to develop your own lake, and make sure your code is tested to run locally (in your own container or virtual machine) before proceeding with automated deployment, as tweaking and debugging an automated deployment is significantly more complex than a local deployment.

## Create your json configuration file

To describe an automated deployment, you need to create a .json file with the following format:

```json=
{
  "forecast_code": "XXX",
  "config_set": "XXX",
  "function": "1",
  "configure_run": "XXX.yml",
  "use_https": "TRUE",
  "aws_default_region": "s3",
  "aws_s3_endpoint": "flare-forecast.org",
  "schedule": "0 */6 * * *"
}
```

User-provided values (you need to configure these):
* "forecast_code" specifies the URL of your own code repository, e.g. "forecast_code": "https://github.com/FLARE-forecast/FCRE-forecast-code"
* "config_set" specifies the configuration set, which is the name of the directory under "configuration" in your code repository from where to download a configuration file. For example, with "config_set": "default" the configuration files need to be present in https://github.com/FLARE-forecast/FCRE-forecast-code/default
* "configure_run" specifies the YAML configuration file from your run; this file should be present in the repository and config_set as per above. For example, with "configure_run": "configure_run.yml" the file https://github.com/FLARE-forecast/FCRE-forecast-code/default/configure_run.yml will be used
* "schedule" specifies when the forecast should run, using the [UNIX cron format](https://en.wikipedia.org/wiki/Cron); for instance, "schedule": "0 */6 * * *" configures your deployment to run every 6 hours, at the top of the hour

Hardwired values for CIBR project team members (make sure you use the pre-configured values below):
* "function" should be set to "1" for CIBR runs (it specifies the FLARE function to run needs to be set to "1" (the automated deployment will sequence the execution of functions 2, 3, and 4 automatically)
* "use_https" should be set to "TRUE" for CIBR runs (it specifies whether HTTPS is used ("TRUE") or HTTP is used ("FALSE") for access to the S3 server)
* "aws_default_region" should be set to "s3" (it specifies the S3 server region)
* "aws_s3_endpoint" should be set to "flare-forecast.org" (it specifies the S3 server's name)

## Generate a pull request for your json file ##

TBD
