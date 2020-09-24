<img src="https://techally-content.s3-us-west-1.amazonaws.com/public-content/lacework_logo_full.png" width="600">


[![lacework](https://circleci.com/gh/scottford-lw/up-and-running-circleci.svg?style=shield)](https://circleci.com/gh/scottford-lw/up-and-running-circleci)
# Up and Running with Lacework and CircleCI
This repository contains reference code from the blog post Up and Running with Lacework and CircleCI, and can be used a reference for integrating Lacework vulnerability scanning into CircleCI pipelines for both container builds, and for base image builds with HashiCorp [Packer](https://www.packer.io/)

## Prereqs
- Lacework Account
- CircleCI Account
- AWS Account (AMI Build with Packer)

## Scanning Packer builds for vulnerabilities with Lacework
This repo contains an Packer template (`ubuntu1804-base.json`) for building an Ubuntu 1804 Amazon Machine image and publishing that image to Amazon. As part of the build process the Lacework Command Line interface is installed which runs a job to generate a package manifest, and submits that manifest to Lacework to scan the host for vulnerabilites. The results of the scan are returned to the console output. The purpose of this example is to show how to get the results in a build process, but leaves determining what to do with the results (i.e. fail the build) to the user. 

In order to use this you will need to configure the following Environment Variables in CircleCI:

- `AWS_ACCESS_KEY_ID`	- AWS Access Key ID
- `AWS_SECRET_ACCESS_KEY`	- AWS Secret Access Key
- `AWS_REGION` - AWS Region to publish AMI
- `LW_ACCOUNT` - Lacework Account Name
- `LW_API_KEY` - Lacework API Key
- `LW_API_SECRET`	- Lacework API Secret

For more information on CircleCI Environment Variables visit the docs [here](https://circleci.com/docs/2.0/env-vars/)

## Scanning Docker Builds for vulnerabilites with Lacework
This repo also contains a simple `Dockerfile` which along with the `.circleci/config.yml` can be built and published to Docker Hub, and then scanned by Lacework for vulnerabilites using the [Lacework CircleCI Orb](https://circleci.com/orbs/registry/orb/lacework/lacework). 

### Environment Variables
You will need to configure the following Environment Variables:
- `DOCKER_LOGIN` - Docker Hub Username
- `DOCKER_PASSWORD` - Docker Hub Password
- `LW_ACCOUNT` - Lacework Account Name
- `LW_API_KEY` - Lacework API Key
- `LW_API_SECRET`	- Lacework API Secret
