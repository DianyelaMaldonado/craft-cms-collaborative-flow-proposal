# Craft CMS Collaborative Flow Proposal ✨
[![N|Solid](https://raw.githubusercontent.com/DianyelaMaldonado/email-base-layout/development/src/assets/BM-logo.png?token=AM5G2YUBVWL2PQKKHN3FG2LBNITGU)](https://heyblackmagic.com/)

> The most important topic when working collaboratively is the database configuration replication between two or more installations. To handle this part we can use the Craft CMS Project Config characteristic. 📌 

## Project Config 🖥
Craft keeps track of each project’s configuration in a central store called **project config**.
As you make changes to system settings (such as create sections, fields, volumes, etc.), Craft will record those setting values to YAML files in a `config/project/` folder. You can then commit those files to your Git repository, just like your templates and front-end resources.

It offers two benefits:

1. You’ll be able to keep track of your project’s changing state over time.
2. You can propagate new changes to other environments (or developers), rather than manually reapplying them.

### What’s Stored in Project Config 📝
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

## Project initialization 🕹
### (Developer 1) 👩‍💻
1. One developer (let's call her/him **DEV1**) will create and configure the GitHub repository in her/his local enviroment as it is normally done, the difference in the configuration is that in the  *`.gitignore`* file the `cms` directory will not be ignored. You can use `gitignore.example` file in this repository.

![alt text](https://github.com/DianyelaMaldonado/craft-cms-collaborative-flow-proposal/blob/development/src/screenshots/git-ignore.png?raw=true)

1. **(DEV1)** will go to `Utilities -> Project Config` and click the `Rebuild` button to ensure that its project config is up to date with settings stored throughout the database.
![alt text](https://github.com/DianyelaMaldonado/craft-cms-collaborative-flow-proposal/blob/development/src/screenshots/rebuild.png?raw=true)
2. ![alt text](https://github.com/DianyelaMaldonado/craft-cms-collaborative-flow-proposal/blob/development/src/assets/database.png?raw=true) Back up the database and share the dump with others developers.
3. ![alt text](https://github.com/DianyelaMaldonado/craft-cms-collaborative-flow-proposal/blob/development/src/assets/git.png?raw=true) Commit and push changes.

### (Developer 2) 👨‍💻
1. Clone the repo.
2. Import the database that was shared to him by the DEV1.
3. Load the site in the browser to ensure it works.

## Propagating changes between developers 💻 🔄 💻

Everytime a developer make changes in her/his local environment, the contents of the `config/project/` folder are updated to reflect those changes. The developer should commit and push those files to the Git repository just like templates, front-end resources, and other project files.
The other developer(s) should pull those changes and import them to her/his local installation in one of two ways:

- From the “Project Config” utility in the control panel.
- By running the `php craft project-config/apply` terminal command.

Either way, Craft will compare the files in the local `config/project/` folder with its already-loaded project config, and apply whatever new changes it finds.

![alt text](https://github.com/DianyelaMaldonado/craft-cms-collaborative-flow-proposal/blob/development/src/assets/project-config.png?raw=true)

##### NOTE: Sensitive Information Could Be Saved in Project Config YAML
Some of your system components may require sensitive information in their settings, such as:
- a Gmail/SMTP password in your email settings
- a secret access key in an AWS S3 volume

To prevent those values from being saved into your YAML files, make sure you’re setting those fields to environment variables.

----

## Git branching ![alt text](https://github.com/DianyelaMaldonado/craft-cms-collaborative-flow-proposal/blob/development/src/screenshots/branching.png?raw=true)

When working collaborativelly, we need to keep an strict order in our git branching.
A branching strategy is a convention or a set of rules that specify when branches get created. It helps teams and developers by describing the naming guidelines of branches and elaborates on what use the branches should have, and so on.
With a lack of appropriate naming conventions, the code maintenance team suffers numerous confusions and complications.
Git branching naming convention supports the organic growth of a codebase in a systematic way. It helps in separating the work strategically.

#### Branching categories 🗂

##### Regular branches 📂
Available permanently in the repository, the naming convention of regular branches is easy and straightforward.

📔 **development**: The main development branch, restricts developers from adding any changes in the master branch directly. Before merging to the master, changes made in the dev branch undergo reviews and tests.

📔 **master**: The default branch available in the Git repository. Team members need to keep the master branch stable and updated. It usually is stable and doesn't allow direct check-in/push. Merging is possible only after code review.

##### Temporary branches 🗃
Team members can create and delete these branches whenever it is required. Supporting branches are used to aid parallel development between team members, ease tracking of features, and to assist in quickly fixing live production problems. Unlike the main branches, these branches always have a limited life time, since they will be removed eventually.

📘 - **Feature Branches:** Feature branches are used when developing a new feature or enhancement which has the potential of a development lifespan longer than a single deployment. <br>
📕 - **Hot Fix:** A hotfix branch comes from the need to act immediately upon an undesired state of a live production version. Additionally, because of the urgency, a hotfix is not required to be be pushed during a scheduled deployment.<br>
📙 - **Bug Fix:** Bug branches differ from feature branches only semantically. Bug branches will be created when there is a bug on the live site that should be fixed and merged into the next deployment.

#### Branch Flow Examples 🔍
- Example One
![alt text](https://github.com/DianyelaMaldonado/craft-cms-collaborative-flow-proposal/blob/development/src/assets/branch-flow-1.png?raw=true)
---
- Example Two <br> <br>
![alt text](https://github.com/DianyelaMaldonado/craft-cms-collaborative-flow-proposal/blob/development/src/assets/branch-flow-2.png?raw=true)

All involved developers will create feature branches to work in an specific area/component of the site. When the changes are ready the developer will export configuration, and will push the YAML files, templates, styles, scripts, etc.

After pushing the changes a merge request will be created from the feature branch to development.

-----
[Let's make some magic](https://heyblackmagic.com/work) 🧙‍♂️🧙✨ MAKING THE INTERNET A HAPPIER PLACE 💫