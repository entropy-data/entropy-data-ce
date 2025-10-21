# Entropy Data (Community Edition)

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fentropy-data%2Fentropy-data-ce%2Fmain%2Fazure%2Fentropy-data-ce.json) [![Deploy to AWS](images/deploytoaws.svg)](https://eu-central-1.console.aws.amazon.com/cloudformation/home?region=eu-central-1#/stacks/create/review?templateURL=https://entropy-data-ce.s3.us-east-1.amazonaws.com/template.yaml)

Entropy Data (Community Edition) is a free version of the [Entropy Data](https://www.entropy-data.com) that you can host yourself.

In the Community Edition, every user can change any data product or data contract.  
If you need advanced role and permission management, SSO, or customizations, consider the [Enterprise Edition](https://www.entropy-data.com/#pricing).

Community support is offered [in Slack in the channel #entropy-data](https://datacontract.com/slack).

Supported Deployments:
- Anywhere that can run a Docker image and offer a postgres database
- [Locally via Docker Compose](https://github.com/entropy-data/entropy-data-ce/blob/main/docker-compose.yaml)
- [On Kubernetes with Helm](https://github.com/entropy-data/entropy-data-helm)
- [On AWS with Cloudformation](https://eu-central-1.console.aws.amazon.com/cloudformation/home?region=eu-central-1#/stacks/create/review?templateURL=https://entropy-data-ce.s3.us-east-1.amazonaws.com/template.yaml)
- [On Azure with bicep template](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fentropy-data%2Fentropy-data-ce%2Fmain%2Fazure%2Fentropy-data-ce.json)

## Demo

Play with our [demo app](https://demo.entropy-data.com/)!


## Getting Started

Entropy Data (Community Edition) is available as Docker image `entropydata/entropy-data-ce` on [Docker Hub](https://hub.docker.com/r/entropydata/entropy-data-ce).

[Deploy to Azure](azure/), [Deploy to AWS](aws/) or start Entropy Data (Community Edition) locally with Docker Compose:

```bash
git clone https://github.com/entropy-data/entropy-data-ce.git
cd entropy-data-ce
docker compose up --detach
```

Now you can access the Entropy Data (Community Edition) at [http://localhost:8081](http://localhost:8081).

> **_NOTE:_**  The Docker Compose configuration uses a dummy mail server, so no mails are actually sent. Configure your SMTP host accordingly as environment variables.


## Requirements

- Docker Resources: 1 CPU and 1 GB of RAM, more is better
- PostgreSQL version 16 or newer
- PostgreSQL with the extensions available: `vector`, `hstore`, `uuid-ossp`
- SMTP server for transactional emails, such as SendGrid, AWS SES, Azure Communication Services email (Office 365 / Exchange is not recommended, as [SMTP Basic Auth is deprecated](https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/deprecation-of-basic-authentication-exchange-online))


## Configuration

Configure an external database and mail server for production use.

| Environment Variable                             | Example                                    | Description                                                                                 |
|--------------------------------------------------|--------------------------------------------|---------------------------------------------------------------------------------------------|
| APPLICATION_HOST_WEB                             | `http://localhost:8081`                    | The host of the application, used e.g., in email templates build URLs to Entropy Data. |
| APPLICATION_MAIL_FROM                            | `Entropy Data <noreply@example.com>`  | The sender email address for Entropy Data emails.                                      |
| SPRING_DATASOURCE_URL                            | `jdbc:postgresql://postgres:5432/postgres` | JDBC URL of the database                                                                    |
| SPRING_DATASOURCE_USERNAME                       | `postgres`                                 | Login username of the database                                                              |
| SPRING_DATASOURCE_PASSWORD                       | `postgres`                                 | Login password of the database                                                              |
| SPRING_MAIL_HOST                                 | `smtp.example.com`                         | SMTP server host                                                                            |
| SPRING_MAIL_PORT                                 | `587`                                      | SMTP server port                                                                            |
| SPRING_MAIL_USERNAME                             |                                            | Login user of the SMTP server                                                               |
| SPRING_MAIL_PASSWORD                             |                                            | Login password of the SMTP server                                                           |
| SPRING_MAIL_PROPERTIES_MAIL_SMTP_AUTH            | `true`                                     | Use basic authentication for SMTP                                                           |
| SPRING_MAIL_PROPERTIES_MAIL_SMTP_STARTTLS_ENABLE | `true`                                     | Ensure that TLS is used                                                                     |

## Deploy on Azure

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fentropy-data%2Fentropy-data-ce%2Fmain%2Fazure%2Fentropy-data-ce.json)

Use the Azure Resource Manager [template](azure/entropy-data-ce.json) to deploy Entropy Data as WebApp, together with a Postgres database in a virtual network.
You need to provide SMTP server configuration.

## Deploy on AWS

[![Deploy to AWS](images/deploytoaws.svg)](https://eu-central-1.console.aws.amazon.com/cloudformation/home?region=eu-central-1#/stacks/create/review?templateURL=https://entropy-data-ce.s3.us-east-1.amazonaws.com/template.yaml)

Use the AWS Cloud Formation [template](aws/template.yaml) to deploy Entropy Data as AppRunner, together with a Postgres database in a virtual network.

## Get help, reporting bugs and feature requests

Community support is offered [in Slack in the channel #entropy-data](https://datacontract.com/slack).

Want to report a bug or request a feature? Open an [issue](https://github.com/entropy-data/entropy-data-ce/issues/new).

## License

The Entropy Data (Community Edition), being made available as a Docker image, is licensed under the [Community License](https://www.entropy-data.com/COMMUNITY-LICENSE.txt).
