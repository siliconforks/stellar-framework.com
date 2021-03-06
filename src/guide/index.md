---
title: Overview
type: guide
order: 1
---

## What is?

Stellar is an action based web framework focused on developing APIs. Each Stellar execution instance can respond to requests from multiply protocols simultaneously, thereby being possible to use the same API in different usage scenario. The framework is written in JavaScript ES6 using [Node.JS](https://nodejs.org/en/). The objective of Stellar is create an easy usability development environment, reusable and scalable, making Stellar an excellent solution not only for small projects but also for enterprise-scale projects.

It is used a system based in actions. This means that all features are represented as actions, you can read more about this actions in a [section](actions.html) dedicated for them.

An execution instance is able to respond to both client requests and process tasks - operations that are performed concurrently in background. Ex: sending an email.


## Supported Protocols

- HTTP
- WebSocket
- TCP

## Architecture

The Stellar core is composed by the _Engine_, a set of Satellites and three different type of servers. The Engine is responsible for loading modules and provide mechanisms that allow _Satellites_ expose their APIs for the rest of the platform, this, so that the logic could be used by other components. The 

Modules are a way to group features of a given area in order to be more easily ported to other projects or to share with the Open Source community.

![Core Architecture](/images/core_arch.png)

## How to Contribute

Both the [documentation](https://github.com/StellarFw/stellar-framework.com) of this website as the [Stellar](https://github.com/StellarFw/stellar) source code is available on GitHub. You can submit pull requests for the `dev` branch, but before, please read carefully the [contribution guide](https://github.com/StellarFw/stellar/blob/dev/CONTRIBUTING.md). All help is welcome! 😉

You can also help using the [issue manager](https://github.com/StellarFw/stellar/issues)  to report bugs, make suggestions or feature requests.

## Structure of an Application

Below is represented the typical directory structure of a Stellar project. This example is a simple API that implements the functionality of a blog.

```
.
├── config
│   └── (project-level settings)
├── manifest.json
├── modules
│   ├── private
│   └── blog
│       ├── actions
│       │   ├── posts.js
│       │   └── comments.js
│       ├── config
│       │   └── comments.js
│       ├── listeners
│       │   ├── del_post.js
│       │   └── new_post.js
│       ├── manifest.json
│       ├── middleware
│       │   └── edit_permission.js
│       ├── models
│       │   ├── post.js
│       │   └── comment.js
│       ├── satellites
│       │   └── something.js
│       └── tasks
│           └── rss.js
└── temp
    └── (temporary files)
```


- **`config`**: Contains project-level settings. These settings override not only the system settings, but also to the modules. Thus, it is shown a very useful feature to configure the application for your usage scenario without having to change the logic of components already developed, making them reusable for other projects.

- **`manifest.json`**: This file contains the project description, consisting of three properties: name, version, and active modules.

- **`modules`**: Contain all the modules that compose the application, which may or may not be used, according to the `modules` property of `manifest.json` file.

  - **`actions`**: Contains files with the implementation of the actions of the modules. These files can be a single action or else a collection of actions.
  
  - **`config`**: It contains the module settings. These settings are loaded according to the module level, thus overlap to the core and settings of the modules of lower priority. It can also contain new settings to control the behavior of the new features added by the module.

  - **`listeners`**: It contains listeners of events that can occur throughout the runtime.

  - **`manifest.json`**: This file contains the description of the module by describing: `id`, `name`, `version`, `description`, `npmDependencies`.

  - **`middleware`**: Contains the `middleware` declaration, which can be used in other modules.

  - **`models`**: Contains the data models declaration, corresponding to the [Mongoose](http://mongoosejs.com) syntax.

  - **`satellites`**: Contains [Satellites](satellites.html).

  - **`tasks`**: Contain the tasks declaration, they are jobs to be run in background asynchronously.

- **`temp`**: Finally, this folder contains temporary files and logs generated by Stellar.

### manifest.json

The **manifest.json** file allows describe the project by name, version, and active modules. Bellow is an example with the format of this file:

```json
{
  "name": "blog",
  "version": "1.0.0",
  "description": "Um sistema simples de blog com suporte a autenticação",
  "modules": [
    "authentication"
  ]
}
```
