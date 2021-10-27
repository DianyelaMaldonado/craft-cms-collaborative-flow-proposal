# Craft CMS Collaborative Flow Proposal ✨
[![N|Solid](https://raw.githubusercontent.com/DianyelaMaldonado/email-base-layout/development/src/assets/BM-logo.png?token=AM5G2YUBVWL2PQKKHN3FG2LBNITGU)](https://heyblackmagic.com/)

> The most important topic when working collaboratively is the database configuration replication between two or more installations. To handle this part we can use the Craft CMS Project Config characteristic.

## Project Config
Craft keeps track of each project’s configuration in a central store called **project config**.

As you make changes to system settings (such as create sections, fields, volumes, etc.), Craft will record those setting values to YAML files in a `config/project/` folder. You can then commit those files to your Git repository, just like your templates and front-end resources.

It offers two benefits:

1. You’ll be able to keep track of your project’s changing state over time.
2. You can propagate new changes to other environments (or developers), rather than manually reapplying them.

### What’s Stored in Project Config
- Asset volumes and named image transforms
- Category groups
- Craft and plugin schema versions
- Craft edition
- Email settings
- Fields and field groups
- Global sets (settings only, not their content)
- GraphQL schemas, and the access settings for the public schema
- Matrix block types
- Plugin editions and settings
- Routes defined in Settings → Routes
- Sections and entry types
- Sites and site groups
- System name, time zone, and status (live/offline)
- Tag groups
- User settings and user groups

## Project initialization
### (Developer 1)
1. One developer (let's call her/him **DEV1**) will create and configure the GitHub repository in her/his local enviroment as it is normally done, the difference in the configuration is that in the  *`.gitignore`* file the `cms` directory will not be ignored. You can use `gitignore.example` file in this repository.

![alt text](https://raw.githubusercontent.com/DianyelaMaldonado/craft-cms-collaborative-flow-proposal/blob/development/src/screenshots/git-ignore.png?raw=true)

1. **(DEV1)** will go to `Utilities -> Project Config` and click the `Rebuild` button to ensure that its project config is up to date with settings stored throughout the database.
2. Back up the database and share the dump with others developers.
3. Commit and push changes.

### (Developer 2)
1. Clone the repo.
2. Import the database that was shared to him by the DEV1.
3. Load the site in the browser to ensure it works.

## Propagating changes between developers

Everytime a developer make changes in a development environment, the contents of the `config/project/` folder are updated to reflect those changes. Commit those files to your Git repository just like your templates, front-end resources, and other project files.


![alt text](https://raw.githubusercontent.com/DianyelaMaldonado/craft-cms-collaborative-flow-proposal/blob/development/src/assets/project-config.png?raw=true)



-----
MAKING THE INTERNET A HAPPIER PLACE 💫
