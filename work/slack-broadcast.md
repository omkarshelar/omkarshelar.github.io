---
title: "Slack Broadcast"
description: "Broadcast messages to multiple Slack channels using webhooks."
back: "/"
---

:link: Web Link : <a href="https://slack.omkarshelar.dev" target="_blank">https://slack.omkarshelar.dev</a>


**The application provides management of the users' Slack Channels and enables them to broadcast the same message to multiple Slack Channels using slack webhooks.**


The application provides users to configure Slack channels and corresponding webhooks. Once configured, the user can then send the same message to multiple slack channels using the web interface.

---

#### GitHub Links :

Angular Frontend :
[https://github.com/omkarshelar/slack-broadcast-frontend](https://github.com/omkarshelar/slack-broadcast-frontend)

Backend Code :
[https://github.com/omkarshelar/slack-broadcast-API](https://github.com/omkarshelar/slack-broadcast-API)

#### API Docs :
[https://documenter.getpostman.com/view/3370668/SzmcbzVN](https://documenter.getpostman.com/view/3370668/SzmcbzVN)

#### Video Screencast :
<iframe width="800" height="500" src="https://www.youtube.com/embed/FwJ3m2wj0aM" frameborder="0" allow="accelerometer; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

#### Architectural Diagram :

![Slack Broadcast Architecture](/assets/slack-broadcast-arch.svg "Slack Broadcast Architecture")

#### Details :
**Frontend :**

The application frontend is written in Angular.
[Materilize CSS](https://materializecss.com/) is used for styling.
AWS Amplify for handling user authentication using AWS Cognito.

**Backend :**

AWS Cognito :
AWS Cognito handles the users authentication using email/password or Social Logins(Google/Amazon).

APIs :
To connect with backend APIs, the Angular application uses ID Token sent from Cognito.
These tokens are checked for validity. If token is valid, the user can then request his/her resources(slack channels).

The database used is Amazon DynamoDB. The backend code runs in AWS Lambda. The code is written using [AWS Chalice](https://github.com/aws/chalice) which provides a simple interface using Python decorators.

#### Application Features :
* Single Sign On using OAuth.
* Verification of user email.
* Completely Serverless deployment.
* Angular application is a Progressive Web Application.

#### What I learned from the Project :
* Implementing OAuth using Authorization Code Grant flow.
* Using AWS Amplify.
* Using Angular HTTP interceptors.
* Deploying code to AWS Lambda using [AWS Chalice](https://github.com/aws/chalice).
* Designing and Querying DynamoDB tables.
