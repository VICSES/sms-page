# SMS-Page

The SMS Page project allows authorized users to send an administrative
page to their unit by sending an SMS to a designated number.

This project consists of three different microservices designed to run
in the Amazon Web Services ecosystem.

There are also a number of AWS Dynamodb tables utilized by this project.

### SMS-Page-Pager

This microservice bridges the Twilio incoming SMS service and the
SES Viper paging service. It runs as an on demand AWS Lambda instance.

### SMS-Page-Rest

This microservice provides a REST API to the project Dynamodb tables.
This allows a management interface to be provided to the paging project.

The REST API is documented at SMS-Page-Rest/api.md

### SMS-Page-Website

This is a static website which uses Javascript to access the SMS-Page-Rest
interface. It provides a management interface to users.

## Installation

### Prerequisites

#### AWS

You must have an AWS account.  Sign up at https://aws.amazon.com/
The usage should sit in the Free Trial tier.  There will be no charge for
the first six months with a small charge for S3 usage after that.

Create an AWS credentials file as described at https://boto3.readthedocs.io/en/latest/guide/configuration.html

#### Twilio

You must have an upgraded Twilio account.  Sign up at https://www.twilio.com/

#### Azure

You must have a Microsoft Azure registered application.

For some reason the SES prevents registering this with an SES account,
so use a different login, create a free one if required.

Registration can be done at https://apps.dev.microsoft.com/ or https://portal.azure.com/.

TODO: Details of application registration


#### Python

You must have Python 3.6 installed or accessible.
On a Debian based system this can be achieved with,
> apt-get install python3.6

### Configure AWS

Run the dynamodb.py script from this repository.
This will generate the required tables.

TODO: Initial login
TODO: IAM requirements?

### Install REST interface

The REST interface will be installed as an AWS Lambda service managed
by zappa.

From within the SMS-Page-Rest repository.

> python3.6 -m venv env
> source env/bin/activate
> pip3.6 install -r requirements.txt
> zappa init

Edit the generated zappa_settings.json file as described in the supplied example_zappa_settings.json file.

> zappa deploy prod

TODO: Domain name

### Install web management interface

TODO

### Install paging service

TODO
