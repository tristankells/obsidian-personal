You manage the deployment of an Azure Container Registry named registry1 for a company.

You need to ensure that registry1 **** can be shared across multiple groups in the company, enabling group isolation.

What should you use?

Select only one answer.

artifact

tag

namespace

**This answer is correct.**

layer

This item tests the candidate’s knowledge of publishing an image to Azure Container Registry. A repository is a collection of container images or other artifacts in a registry that have the same name but different tags. A namespace enables the identification of related repositories and artifact ownership by using forward slash-delimited names. A tag for an image specifies its version. An artifact can be, for instance, a text file, a docker image, or a Helm chart stored in the registry with one or more tags. Container images consist of layers. Layers are used to avoid transferring redundant information and to skip build steps that have not changed.

[Manage container images in Azure Container Registry](https://learn.microsoft.com/training/modules/publish-container-image-to-azure-container-registry/)

---
You develop a web application hosted on the Web Apps feature of Microsoft Azure App Service.

You need to enable and configure Azure Web Service Local Cache with 1.5 GB.

Which two code segments should you use? Each correct answer presents part of the solution.

Select all answers that apply.

`“WEBSITE_LOCAL_CACHE_OPTION”: “Always”`

**This answer is correct.**

`“WEBSITE_LOCAL_CACHE_SIZEINMB”: “1500”`

**This answer is correct.**

`“WEBSITE_LOCAL_CACHE_OPTION”: “Enable”`

**This answer is incorrect.**

`“WEBSITE_LOCAL_CACHE_SIZEINMB”: “1.5”`

This item tests the candidate’s knowledge of configuring the settings of the Web Apps feature of Azure App Service.

By using `WEBSITE_LOCAL_CACHE_OPTION = Always`, local cache will be enabled. `WEBSITE_LOCAL_CACHE_SIZEINMB` will properly configure Local Cache with 1.5 GB of size. `WEBSITE_LOCAL_CACHE_OPTION = Enable` is not a valid value. `1.5` will not configure 1.5 GB for the local cache.

[Configure web app settings - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/configure-web-app-settings/)