Azure Deployment Template
===

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fentropy-data%2Fentropy-data-ce%2Fmain%2Fazure%2Fentropy-data-ce.json)

This deployment templates can be used to deploy Data Mesh Manager to Azure.

It is coded as a [bicep file](entropy-data-ce.bicep), and comes with a generated [Azure Resource Manager template](entropy-data-ce.json) that can be used directly in Azure deployments.

Use it directly as a deployment templates, or copy it to configure to your custom needs.

Resources
---

As defined in the [bicep file](entropy-data-ce.bicep), these resources will be created:

- WebApp that runs the Docker image
- Postgres Database
- Virtual Network (Postgres is not exposed to public internet)

The application will be available under

https://${webAppName}.azurewebsites.net


Configuration
---

You need to provide credetials for an SMTP mail server. If you don't have one, you can use [Azure Communication Service](https://learn.microsoft.com/en-us/azure/communication-services/quickstarts/email/send-email-smtp/smtp-authentication) or (SendGrid)[https://portal.azure.com/#create/sendgrid.tsg-saas-offer].



Development
---

Compile bicep file to Azure Resource Manager template 

```
az bicep build --file entropy-data-ce.bicep --outfile entropy-data-ce.json
```


Get help, reporting bugs and feature requests
--

Community support is offered [in Slack in the channel #entropy-data](https://datacontract.com/slack).

Want to report a bug or request a feature? Open an [issue](https://github.com/entropy-data/entropy-data-ce/issues/new).
