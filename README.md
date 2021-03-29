# DEPTH DROP MASTER SERVER GUIDE

## INSTALLING DEPENDENCIES

1. Make sure you're on nodejs v6 LTS (in a command prompt run the command `node --version`, should read "v6.x.x", this is correct).
2. Update npm `npm install -g npm`
3. Install typings `npm install -g typings`
4. Install gulp `npm install -g gulp`
5. Use npm to install dependencies `npm install` << run this in the trunk directory of the project where the package.json file resides. This command will read that package.json file and install the appropriate libraries.
6. Use typings to install typings dependencies `typings install` << run this in the trunk directory of the project where the typings.json file resides. This acts similarly to `npm install`

## WORKING WITH THE PROJECT

Make sure to edit the project in **Visual Studio Code** (*VSC*). This version was actively worked on using VSC 1.11.1.

You'll want to download the following plugins for VSC :

1. TSLint
2. TODO Parser -- this needs to be manual run if you want to get the current TODOs, very helpful.
3. TortoiseSVN -- If you have the TortoiseSVN desktop client then this has handy bindings to it.

## BUILDING

You'll need some things before you can build a running version of the code. You'll need to copy the `Depth-Infrastructure-ENV.key` file from `\\Dicocentral\dico\Projects\Depth\DropMaster\secrets\YOURENVIRONMENT\` to `config\YOURENVIRONMENT\` before the build will work within dev or live.

Building this application is very simple
1. simply open the `DropMasterServer` folder with visual studio code.
2. Press Control+P
3. Start typings `task ` (don't forget the space). This should show a list of tasks available to run
4. Select build-dev, build-local or build-live depending on the environment you want to build the application for. This will run automated tslinting, tsc, copying of appropriate files and zipping the project for deployment.
5. That's it, the application is build, there should be a zip in the ./build/ folder.

## DEPLOYING

Before you can deploy your code to elastic bean stalk you need the appropriate `config.aws.json` file from `\\Dicocentral\dico\Projects\Depth\DropMaster\secrets\YOURENVIRONMENT\` and copy it to `secrets\YOURENVIRONMENT\` before the EB deploy code will work.

Currently you can only deploy the application from the command line. 
1. start a command prompt in the `DropMasterServer` folder.
2. Depending on your environment run the command `gulp push-ENV --ENV` where ENV is either `dev` or `live` (local is not supported as you don't deploy local versions).
3. That's it, watch as gulp deploys your program to elastic beanstalk.

## PROJECT STRUCTURE

This section explains the folder structure of the project.

* build/	      : When you run the build task this is where the builds are stored. There are separate folders in here for different build enviroments. Zipped version of these folders will be stored in the root of build/
* config/         : This is where the configuration files are stored, there are per environment configuration files and a default configuration file
* secrets/        : This folder contains files that ARE NOT stored on SVN for security purposes. If you want to build and deploy the app you'll need to get the appropriate files to put in this folder first before proceeding (do NOT add them to SVN).
* src/	          : This is where the source code (.ts files) are stored for the project. There should be no .js files in this folder.
* srcmaps/        : This folder contains the mappings from .ts file to .js files that are generated during a build. These are important as they will be used with the source-mappings pluging to reference line numbers in the .ts files when an error occurs and a stack trace is produced.
* typings/        : The typings used in this project.
* static_content/ : This folder contains folders and files that will be copied into the root of any build of the project, files that don't need compilation and are not going to change. .js files are considered static.

