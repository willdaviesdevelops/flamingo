# flamingo
flamingo is a web-based service that allows the management of language-driven elements like strings and other assets.  Consider this a replacement for the cumbersome resx files and simple database table solutions commonly used in some web applications.  Rather than use static files like xml (.resx) or a simple database table with clunky calls to resolve key/value pairs, Flamingo allows its users a way to manage these values in a more efficient way.

## AWS For The Win 
The goal is a completely *serverless* solution using these core services:
* [Route53](https://aws.amazon.com/route53/) - DNS and Domain Registration
* [CloudFront](https://aws.amazon.com/cloudfront/) - CDN (content delivery network) - This service will initially serve content from cache before requesting the content from the content's origin.  In our case, this is S3, DynamoDB or other AWS service.
* [Lambda@Edge](https://aws.amazon.com/lambda/edge/) - Serverless compute at the CDN edge.  
* [S3](https://aws.amazon.com/s3/) - Storage.  This will provide the static content for the site.  It will also hold the other artifacts like the Lambda source code.
* [Amazon API Gateway](https://aws.amazon.com/api-gateway/) - A customizable interface for interacting with additional backend services.  It also offers caching for a modest price.
* [Lambda](https://aws.amazon.com/lambda/) - Serverless compute run on-demand.  The bulk of the work will be in C#, although there will also be some Node.js for simple functions.
* [DynamoDB](https://aws.amazon.com/dynamodb/) - NoSQL database as a service.  This will be the repository for our language entries.

### Additional AWS Services to support the application
* [SNS](https://aws.amazon.com/sns/) - Pub/sub messaging. Notification service to send notifications (messages) to Lambda, triggering a function call or notifying another service or user of something.
* [SQS](https://aws.amazon.com/sqs/) - Queueing service to de-couple other services from each other.
* [STS](https://aws.amazon.com/documentation/iam/) - Simple Token Service - Temporary credentials for accesss to AWS resources: [STS CLI Reference](http://docs.aws.amazon.com/cli/latest/reference/sts/index.html) | [STS API Reference](http://docs.aws.amazon.com/STS/latest/APIReference/Welcome.html)

## Additional Web Services, Frameworks:
* [Auth0](https://auth0.com/) - Authentication service using social providers.
* [Bootstrap](http://getbootstrap.com/) - UI: HTML, CSS, JS
* [Stripe](https://stripe.com/) - Commerce platform.  Payment and subscription management.

## Goals for the Project

#### What should it do (for the applications that use it and the people that use it?
* Apps that use the service expect:
  * To give the service a key and return a value
  * To give the service a set of keys and return a set of values
  * To give the service a key that represents a set of values (allow grouping of commonly consumed values)
* People that manage these values expect:
  * To be able to manage values stored in the system (CRUD)
  * Allow some people to review values but not change them (Authorization)
  * Audit the values for activity (hot values, cold values)
  * Create and manage test pages with keys and values

#### Project Parts
* Content: HTML, CSS, Js, Images and other content
* CloudFormation templates
* Application package files ([*Serverless*](https://serverless.com/), [SAM](https://github.com/awslabs/serverless-application-model), etc.)
* Code - C#, node.js, and other code elements

#### Project Organization
* Questions:
  * Will it be one repo to rule them all or several repos revolving around various concerns?
  * Will it use online services like Jira in the cloud, or will it use AWS-only services like CodeBuild, CodeDeploy, and others?
