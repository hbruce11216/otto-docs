# AWS Architecture

![AWS Architecture Diagram](/images/otto-aws.png "Otto AWS Architecture")

## Services
* **AWS S3** - Used for serving the front-end web application and used for storing CSV uploads and batch processing CSV results.
* **API Gateway** - All front-end HTTP requests are served by AWS API Gateway REST APIs wired to Lambda functions
* **AWS Lambda** - Used to serve API requests and business logic such as LinkedIn profile scraping and Google article search
* **DynamoDB** - Used as a database following a single-table design
* **AWS Comprehend** - Used for detecting keyphrases in a scraped LinkedIn Profile
* **AWS IOT** - Used for real-time results publication via MQTT. MQTT topics are named using the AWS Request ID (e.g. `otto/requests/[request id]`)
* **Amazon Simple Email Service (SES)** - Used for sending email notifications.