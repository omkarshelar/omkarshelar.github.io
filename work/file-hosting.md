---
title: "File Hosting"
description: "Ephemeral file hosting Web and CLI applications"
---
:link: Web Link : <a href="https://filehosting.omkarshelar.dev" target="_blank">https://filehosting.omkarshelar.dev</a>

**Quickly share your files with others. Upload a file and the application generates a link that can be shared with others. The application deletes the files after a user specified time.**

---

#### GitHub Links :
<i class="fa fa-github" aria-hidden="true"></i>
	[Web Application Repository](https://github.com/omkarshelar/file-hosting-frontend)

<i class="fa fa-github" aria-hidden="true"></i>
	[Backend Repository](https://github.com/omkarshelar/file-hosting-backend)
	
<i class="fa fa-github" aria-hidden="true"></i>
	[CLI Repository](https://github.com/omkarshelar/file-hosting-cli)


**Here's a quick demo of the CLI application**
<asciinema-player src="/assets/demo.cast" poster="npt:00:03" speed="1.5" rows="40" cols="120"></asciinema-player>

#### Architectural Diagram :
![File Hosting Architecture](/assets/File-Hosting-App.svg "File Hosting Architecture")

#### Details :
**Frontend :**
The frontend application is writeen in Typescript with [ParcelJS bundler](https://parceljs.org/).

**APIs :**
Written using AWS chalice. The datastore used is DynamoDB.

**CLI Tool :**
CLI is written in node. Can be run using `npx fha` command.
**Please note :** that the CLI tool requires API key to prevent misuse of the application and keep hosting costs low.

<script src="/assets/asciinema-player.js"></script>