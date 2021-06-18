# Auto-Deploy Superpowers

## Introduction

In this project, we prove mastery of the following objectives:

  - Explain the fundamentals and benefits of CI/CD to achieve, build, and deploy automation for cloud-based software products
  - Utilize deployment strategies to design and build CI/CD pipelines that support Continuous Delivery processes
  - Utilize a configuration management tool to accomplish deployment to cloud-based servers
  - Surface critical server errors for diagnosis using centralized structured logging

## Selling CI/CD

You're leading a team to develop the *UdaPeople* product, a revolutionary concept in Human Resources which promises to help small businesses care better for their most valuable resources: their people. Before implementing CI/CD for the UdaPeople product, you need to get authorization from the people who write the checks.

Translate the benefits of CI/CD from technical language to the values of the business. To appeal to what makes business people tick, you'll need to focus attention on benefits that create revenue, protect revenue, control costs or reduce costs.

**Deliverable**

Your presentation should be no longer than 5 slides (your boss likes presentations that are short and sweet).

The presentation should be in PDF format (e.g. `presentation.pdf`) and should be included in the code repo's root folder.

## Getting Started

### Starter Code

  1. Clone the [starter code](https://github.com/udacity/cdond-c3-projectstarter)
  2. Push the clone to a new repo in your account
    - NOTE: It might help to make the repo public so that Circle CI will give you more credits to run builds ([more info here](https://circleci.com/open-source/))

### Provided Cloud Formation Templates

CloudFormation templates are provided in [this folder](https://github.com/udacity/cdond-c3-projectstarter/tree/master/.circleci/files) to use throughout the deployment phase.

### Intentionally Failing Jobs

A `config.yml` file is provided [here](https://github.com/udacity/cdond-c3-projectstarter/blob/master/.circleci/config.yml) to help get started with Circle CI's configuration. To call attention to unfinished jobs, "non zero error codes" (e.g. `exit 1`) are there to be removed when an implementation is finished.

### OPTIONAL: Compiling/Running Locally

It is NOT necessary to compile and run this project locally. The goal of this project is to **show mastery in management of CI/CD systems**, not React/NodeJS web applications.

> **NOTE**
>
> If you are experienced with React/NodeJS or don't mind an extra challenge, then compile away!

The instructions and information that follow should help build, test, and deploy the web application either locally or in CI/CD.

This is a *mono-repository*, meaning multiple servers or layers exist in the same repo. The following main folders are:

  - `./frontend`

  - `./backend`

### Environment Setup

**1. Install dependencies on both `fronted` and `backend` folders**

From the `cdond-c3-projectstarter` folder, use the commands:

```shell
cd frontend

npm i
```

From the `cdond-c3-projectstarter` folder, use the commands:

```shell
cd backend

npm i
```

**2. Create `.env` file for database connection info**

Add a `.env` file to your `backend` folder with the following contents:

```shell
NODE_ENV=local
VERSION=1
TYPEORM_CONNECTION=postgres
TYPEORM_MIGRATIONS_DIR=./src/migrations
TYPEORM_ENTITIES=./src/modules/domain/**/*.entity.ts
TYPEORM_MIGRATIONS=./src/migrations/*.ts

# Things you can change if you wish...
TYPEORM_HOST=localhost
TYPEORM_PORT=5532
TYPEORM_USERNAME=postgres
TYPEORM_PASSWORD=password
TYPEORM_DATABASE=glee
```

> **NOTE**
>
> You can use your own Postgres server if you wish or you can use the Docker-Compose template provided in the `./util` folder.

### Running PostgreSQL in Docker-Compose

For convenience, a template is provided to easily run a Postgres database for local testing. To run this template, install Docker and Docker-Compose.

To start the database, use the following commands from `cdond-c3-projectstarter`:

```shell
cd util

docker-compose up
```

### Compiling the Code

You can compile the code from `cdond-c3-projectstarter` using the following:

```shell
cd frontend
npm run build
```

> **NOTE**
>
> There are some errors in both `frontend` and `backend` that will make any attempt to compile FAIL when you first clone the repo. These errors are *intentional*. There are steps in the project that require a build to break in Circle CI.
>
> Don't fix the errors until instructed to do so.

### Testing, Migrating, Running

As stated in the note, most of the code in the project won't be possible to run until later on when errors are instructed to be fixed. The following commands are provided for reference, but may fail upon initial run.

Most tasks needed to build, test, and deploy the application are simplified by "npm scripts" that are found in `package.json` for either `frontend` or `backend`. For any of these scripts, you'll need to `cd` into the respective folder and then run the script using `npm run [script name]`.

Here are some relevant scripts:

<table>
    <tr>
        <th>Name</th>
        <th>Purpose</th>
        <th>Notes</th>
    </tr>
    <tr>
        <td>migrations</td>
        <td>Run migration which checks for any migration scripts that have not yet been applied to the db and runs them.</td>
        <td>Make sure you have a Postgres database running and your <code>.env</code> file is configured correctly. If you get connection errors from the backend when you start it, then chances are your DB is not running or the <code>.env</code> doesn't have the correct DB connection information.</td>
    </tr>
    <tr>
        <td>migrations:revert</td>
        <td>Revert last successfully executed migrations.</td>
        <td>The same connection configuration is needed here as with the <code>migrations</code> script above.</td>
    </tr>
    <tr>
        <td>test</td>
        <td>Run all unit tests.</td>
        <td></td>
    </tr>
    <tr>
        <td>build</td>
        <td>Compiles the code.</td>
        <td>Drops the compiled code in the <code>./dist</code> folder.</td>
    </tr>
    <tr>
        <td>start</td>
        <td>Starts up the application locally.</td>
        <td>Make sure you have a Postgres database running and your <code>.env</code> file is configured correctly. If you get connection errors from the backend when you start it, then chances are your DB is not running or the <code>.env</code> doesn't have the correct DB connection information.</td>
    </tr>
</table>

### Examples

This should compile the code and then list the result in the `./dist` folder:

```shell
cd frontend
npm run build
cd dist
ls
```

Or revert the last migration that ran:

```shell
cd backend
npm run migrations:revert
```

## Deploying Working, Trustworthy Software

### Circle CI

Circle CI is a SaaS and has a [free account](https://circleci.com/signup/?source-button=free) to be used throughout the project (ideal since UdaPeople is on a shoestring budget).

  1. [Create an account](https://circleci.com/signup/?source-button=free) if you haven't already.

    - There are 2500 credits per week (about 70 builds)
    - *If you run out of credits, you can create another account*

  2. Create a new project using your Github repo.

    - The `.circleci` folder is where jobs will go

  3. Ensure a workflow starts with the jobs in the `.config` file

    - Circle CI has [a few samples](https://circleci.com/docs/2.0/sample-config)

### Screenshots and URLs

Throughout this project, screenshots or URLs will be needed for the evaluation process.

### 1. Build Phase

The goal of the build phase is to compile or *lint* the source code to check for syntax errors or unintentional typos in code. It's the first line of defense against bugs as you attempt to integrate the pieces of your project together. This is especially important to *UdaPeople* because we don't want to waste credits or time running other steps if the code can't even compile.

### 2. Test Phase

Unit tests are one of the many very important building blocks of a system that enables Continuous Delivery. *UdaPeople* believes that tests should come first just like they do in the scientific method. If a test fails, it's because the code is no longer trustworthy. Only trustworthy code should get a ticket to continue the ride!
