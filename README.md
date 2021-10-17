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

### 3. Analyze Phase

*UdaPeople* handles some private information like social security numbers, salary amount, etc. It would be a shame if a package with a known vulnerability left a security hole in our application, giving hackers access to that information! That's why we should include a job that checks for known vulnerabilities every time we check in new code.

### 4. Alerts

When a build fails for any reason, the *UdaPeople* dev team needs to know about it. That way they can jump in and save the day.

## Configuration Management

In this section, we practice creating and configuring infrastructure before deploying code to it. We accomplish this by preparing our AWS and CircleCI accounts just a bit, then by building Ansible Playbooks for use in our CircleCI configuration.

### Setup

**AWS**

1. Create a [new key pair](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html#having-ec2-create-your-key-pair) for CircleCI to use to work with AWS resources.

2. Create an [IAM user with *programmatic access*](https://serverless-stack.com/chapters/create-an-iam-user.html) and copy the id and access keys (these credentials will be needed for CircleCI to run AWS CLI commands).

3. Add a [PostgreSQL database in RDS](https://aws.amazon.com/getting-started/tutorials/create-connect-postgresql-db/) that has *public accessibility*.

  - Take note of connection details (*hostname* - aka endpoint, username, password)

  - As long as *public accessibility* is marked as *yes*, you won't need to worry about VPC settings or security groups

For this version, the postgres credentials are:

  - db instance &mdash; udapeople-prod
  - username &mdash; postgres
  - password &mdash; udapeople123
  - db port &mdash; 5432 (default for any postgres database)

### CloudFront Distribution Primer

At the very end of the pipeline, you'll need to make a switch from the old infrastructure to the new (Blue Green Deployment strategy). We will use CloudFormation and CloudFront to accomplish this. For this to work, a few things are done manually:

  1. Create a random string (e.g. `kk1j287dhjppmz437`) for use in the next steps

  2. Create an S3 bucket with a name that combines "udapeople" and the random string (e.g. `udapeople-kk1j287dhjppmz437`)

    - If S3 complains that the name is already taken, just choose another random string

    - The random string is to distinguish your bucket from other buckets

  3. Run the provided [Cloud Formation](https://github.com/udacity/cdond-c3-projectstarter/blob/master/.circleci/files/cloudfront.yml) template locally (for the Workflow ID parameter, use your random string)

The method below was used to generate a random string:

```python
>>> import random
>>> import string
>>>
>>> random_string = ''
>>> for i in range(2):
...     random_string += ''.join(random.choice(letters) for j in range(5))
...     random_string += ''.join(random.choice(digits) for j in range(3))
```

For this version, `qyznd553hoiiu818` will be the random string.

Use this command to run the Cloud Formation template:

```shell
aws cloudformation create-stack --stack-name udapeople-stack --template-body file://.circleci/files/cloudfront.yml --parameters ParameterKey=WorkflowID,ParameterValue=qyznd553hoiiu818 --profile udacity-devops-default
```

Once this is done, subsequent executions of that template will modify the same CloudFront distribution to make the blue-to-green switch without fail.

### Circle CI

1. Add SSH key pairs from EC2 as shows [here](https://circleci.com/docs/2.0/add-ssh-key/).

  - To get the actual key pair, you'll need to open the pem file in a text editor and copy the contents, then paste them into Circle CI (you can use `cat path/to/pem-file.pem` to just print the contents)

2. Add the following environment variables to your Circle CI project by navigating to `{project name}` > Settings > Environment Variables, as shown [here](https://circleci.com/docs/2.0/settings/):

  - `AWS_ACCESS_KEY_ID` &mdash; from IAM user CSV file

  - `AWS_SECRET_ACCESS_KEY` &mdash; from IAM user CSV file

  - `AWS_DEFAULT_REGION` &mdash; your default AWS region

  - `TYPEORM_CONNECTION` &mdash; `postgres`

  - `TYPEORM_MIGRATIONS_DIR` &mdash; `./src/migrations`

  - `TYPEORM_ENTITIES` &mdash; `./src/modules/domain/**/*.entity.ts`

  - `TYPEORM_MIGRATIONS` &mdash; `./src/migrations/*.ts`

  - `TYPEORM_HOST` &mdash; the postgres database hostname in RDS

  - `TYPEORM_PORT` &mdash; `5432` (or RDS port if it's different)

  - `TYPEORM_USERNAME` &mdash; your postgres database username in RDS

  - `TYPEORM_PASSWORD` &mdash; your postgres database password in RDS

  - `TYPEORM_DATABASE` &mdash; your postgres database name in RDS

> **NOTE**
>
> Some AWS-related jobs may take a while to complete. If a job takes too long, it could cause a timeout. If this is the case, just restart the job and keep your fingers crossed for faster network traffic. If this happens often, you might consider [increasing the job timeout](https://support.circleci.com/hc/en-us/articles/360007188574-Build-has-hit-timeout-limit).

### 1. Infrastructure Phrase

Setting up servers and infrastructure involves many moving parts and points of failure. UdaPeople has adopted the IaC philosophy so that the team never has to worry about a missed deployment checklist item.

In this phase, we add Circle CI jobs that execute Cloud Formation templates that create infrastructure as well as jobs that execute Ansible Playbooks to configure that newly created infrastructure.

### 2. Deploy Phase

With infrastructure up and running, we can configure dependencies and move applications over. *UdaPeople* used to have an ops guy to make copies every Friday, but now they want to make a full deploy on every single commit. Luckily for UdaPeople, you can add a job that handles this automatically with Ansible.

### 3. Smoke Test Phase

What if the UdaPeople website is down due to a runtime bug that our unit tests didn't catch? The first thing we do after deploying is run a smoke test to make sure we have access to all our created resources.

### 4. Rollback Phase

Any experienced developer knows that not every pipeline follows the "happy path." If the smoke test fails, what should we do?

The `destroy-environment` command removes infrastructure if something goes wrong:

    - Trigger rollbacks if the smoke tests or any following jobs fail
    - Delete files uploaded to S3
    - Destroy the current CloudFormation stacks

The `revert-migrations` command rolls back any migrations that were successfully applied during this CI/CD workflow:

    - Trigger rollbacks if the smoke tests or any following jobs fail
    - Revert the last migration (IF a new migration was applied) on the database so that it goes back to the way it was before

No more jobs should run after these commands have executed.

### 5. Promotion Phase

Assuming smoke tests came back clean, we should have a relatively high level of confidence that our deployment was a 99% success. Now it's time for the last 1%. *UdaPeople* uses the "Blue-Green Deployment Strategy" which means we deployed a second environment or stack next to our existing production stack. Now that we're sure everything is "A-okay", we can switch from blue to green.

### 6. Cleanup Phase

The *UdaPeople* finance department likes it when AWS bills are more or less the same as last month OR trending downward. But, what if this "Blue-Green" strategy is leaving behind a trail of dead-end production environments? We avoid this upward cost trend by adding a cleanup job for the old stacks.

### Other considerations

## Troubleshooting

### Run Migrations

If the project is left alone for a long time and a CircleCI rebuild happens, the `run-migrations` step sometimes fails. If this happens, do the following:

  1. Reset the default password in the RDS database

    - Click the database name you wish to modify
    - Click the "Modify" button
    - Enter a new password (or re-enter the old one) in the "New master password" field
    - Check the box to propagate this change immediately

  2. Reset (delete and re-enter) the [Project Environment Variables](https://app.circleci.com/settings/project/github/rtelles64/udacity_autodeploy_project/environment-variables?return-to=https%3A%2F%2Fapp.circleci.com%2Fpipelines%2Fgithub%2Frtelles64%2Fudacity_autodeploy_project%3Fbranch%3Dmain) in CircleCI

Once the steps above have been completed, initiate a new CircleCI rebuild.

### Deploy Backend

**Timeout**

Occasionally, the `deploy-backend` step fails. This is typically because of server lags on Amazon's side. CircleCI issues a timeout if a job takes too long to complete.

Simply initiate a new CircleCI rebuild.
