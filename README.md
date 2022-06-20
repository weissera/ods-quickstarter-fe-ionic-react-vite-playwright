# OpenDevStack - Quickstarter - Frontend Ionic React

> An advanced OpenDevStack Frontend Quickstarter to build mobile and desktop apps with the ionic framework and react.

![Version](https://img.shields.io/badge/version-1.0.4-blue.svg?style=for-the-badge&cacheSeconds=2592000)
[![License: Apache-2.0](https://img.shields.io/github/license/simongolms/ods-jenkins-agent-nodejs?style=for-the-badge)](https://github.com/simongolms/ods-jenkins-agent-nodejs/blob/master/LICENSE)
[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg?style=for-the-badge)](https://github.com/simongolms/ods-jenkins-agent-nodejs/graphs/commit-activity)
[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-green.svg?style=for-the-badge)](https://conventionalcommits.org)
![Prerequisite Npm](https://img.shields.io/badge/npm-%3E%3D8.5.5-blue.svg?style=for-the-badge)
![Prerequisite Node](https://img.shields.io/badge/node-%3E%3D16.15-blue.svg?style=for-the-badge)

## Features

- Ionic/React with Typescript for building cross-platform native and web app
- Single-Sign-On (SSO) for user authentication and authorization with Azure Active Directory
- OpenDevStack (ODS) CI/CD configuration out of the box with the basic setup for Docker (incl. injecting Runtime Variables), Jenkins (incl. feature environments, release-manager rollout) and OpenShift (managed with Helm)
  - Ionic Appflow (coming soon)
- Setup for ESlint, Stylelint, Prettier, commitlint, Husky (git hooks) and semantic versioning for a better developer experience

---

<!-- Feel free to delete the section 'Provision Quickstarter' after you successfully provisioned the quickstarter -->

## Provision Quickstarter

For an official ODS Quickstarter, the provisioning app takes care of the provisioning in combination with the Jenkinsfile in the associated Quickstarter template.
However, since this is an extended Quickstarter, which is developed independently and decoupled from ODS, the necessary steps of the provisioning app and Jenkins itself must be performed, which are covered in this section.

### Prerequisites

To provision this Quickstarter, you need a deployed ODS project with the corresponding `*-cd`, `*-dev` and `*-test` projects in the OpenShift 4 dev cluster, the `*-prod` project in the OpenShift 4 prod cluster and the associated Bitbucket project.

### Setup Quickstarter

#### 1. Get Source Code

- Option 1 (recommended): Clone the repository

  ```sh
  git clone https://github.com/SimonGolms/ods-quickstarter-fe-ionic-react.git
  cd ods-quickstarter-fe-ionic-react
  ```

- Option 2: Download the repository

  ```sh
  curl --location --remote-name https://github.com/SimonGolms/ods-quickstarter-fe-ionic-react/archive/refs/heads/main.tar.gz && \
  tar -xvzf main.tar.gz && \
  rm main.tar.gz
  cd ods-quickstarter-fe-ionic-react-main
  ```

#### 2. Set Project Id

To make the Quickstarter available in your project, the corresponding project id is required. With the following command all files are checked. The placeholder `foo` is searched and replaced by the actual project id.

Replace `YOUR_PROJECT_ID` with your project id, e.g. `foo`

```sh
# IMPORTANT: Keep your project id in lowercase.
find . -type f -exec sed --expression 's/foo/YOUR_PROJECT_ID/g' --in-place {} +
```

🛑 **IMPORTANT:** This and the other commands also replace the placeholders in the other sections of the documentation. It is therefore recommended to continue with the README in the downloaded source code. Otherwise, please be aware that you have to replace the placeholder `foo` with your project id for each further command.

#### 3. Set Component Id

Replace `YOUR_COMPONENT_ID` with your component id, e.g. `app`, `frontend`, etc.

```sh
# IMPORTANT: Keep your component id in lowercase.
find . -type f -exec sed --expression 's/app/YOUR_COMPONENT_ID/g' --in-place {} +
```

#### 4. Set OpenShift dev domain URLs

Replace `YOUR_OPENSHIFT_DOMAIN_DEV` with your OpenShift 4 Dev Cluster Domain, e.g. `dev.ocp.company.com`

<details><summary>How do I find out the <code>YOUR_OPENSHIFT_DOMAIN_DEV</code> value?</summary>

Go to your `*-cd` project of your OpenShift 4 Dev Cluster in the browser and look at the URL properly. Extract the `YOUR_OPENSHIFT_DOMAIN_DEV` as follows:

```txt
https://console-openshift-console.apps.dev.ocp.company.com/topology/ns/foo-cd ◄── Your url

https://console-openshift-console.apps.   dev.ocp.company.com   /topology/ns/foo-cd
                  ▲                                 ▲                     ▲
                  │                                 │                     └─── Pathname
                  │                                 └── YOUR_OPENSHIFT_DOMAIN_DEV
                  └─ Application Sub Domain
```

</details>

```sh
find . -type f -exec sed --expression 's/OPENSHIFT_DOMAIN_DEV/YOUR_OPENSHIFT_DOMAIN_DEV/g' --in-place {} +
```

#### 5. Set OpenShift prod domain URLs

Replace `OPENSHIFT_DOMAIN_PROD` with your OpenShift 4 Dev Cluster Domain, e.g. `prod.ocp.company.com`

<details><summary>How do I find out the <code>YOUR_OPENSHIFT_DOMAIN_PROD</code> value?</summary>

Go to your `*-prod` project of your OpenShift 4 Dev Cluster in the browser and look at the URL properly. Extract the `YOUR_OPENSHIFT_DOMAIN_PROD` as follows:

```txt
https://console-openshift-console.apps.dev.ocp.company.com/topology/ns/foo-cd ◄── Your url

https://console-openshift-console.apps.   dev.ocp.company.com   /topology/ns/foo-cd
                  ▲                                 ▲                     ▲
                  │                                 │                     └─── Pathname
                  │                                 └── YOUR_OPENSHIFT_DOMAIN_PROD
                  └─ Application Sub Domain
```

</details>

```sh
find . -type f -exec sed --expression 's/OPENSHIFT_DOMAIN_PROD/YOUR_OPENSHIFT_DOMAIN_PROD/g' --in-place {} +
```

#### 6. Set BitBucket domain URL

Replace `YOUR_BITBUCKET_DOMAIN` with your BitBucket Domain, e.g. `bitbucket.company.com`

<details><summary>How do I find out the <code>YOUR_BITBUCKET_DOMAIN</code> value?</summary>

Go to your BitBucket project in the browser and look at the URL properly. Extract the `YOUR_BITBUCKET_DOMAIN` as follows:

```txt
https://bitbucket.company.com/projects/foo ◄── Your url

https://   bitbucket.company.com   /projects/foo
  ▲                ▲                     ▲
  │                │                     └─── Pathname
  │                └── YOUR_BITBUCKET_DOMAIN
  └─ Protocol
```

</details>

```sh
find . -type f -exec sed --expression 's/BITBUCKET_DOMAIN/YOUR_BITBUCKET_DOMAIN/g' --in-place {} +
```

#### 7. Remove template resources

```sh
rm -rf .git .github CHANGELOG.md
```

#### 8. Install `helm` cli

[Helm](https://helm.sh/) is a package manager for Kubernetes that configures and deploys applications and services on a Kubernetes/OpenShift cluster. Think of it like `apt`/`yum`/`homebrew` for Kubernetes. It uses Helm charts to simplify the development and deployment process.

`helm` will be used later in the [`pre-commit`](./.husky/pre-commit) git hook for linting the application [Helm charts](./chart/).

```sh
# Install helm cli
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

# Verify successfully installed helm version
helm version
```

More Information: <https://helm.sh/docs/intro/install/>

#### 9. Install `oc` cli

With the OpenShift command-line interface (CLI), the `oc` command, you can create applications and manage OpenShift Container Platform projects from a terminal.

`oc` will be used by helm and for further configuration and housekeeping tasks.

To be compatible with the latest OpenShift Container Platform (OCP) version, the binary is downloaded and installed from the associated OpenShift Container Platform.

```sh
# Install oc cli
curl -O https://downloads-openshift-console.apps.OPENSHIFT_DOMAIN_DEV/amd64/linux/oc.tar && \
tar -xvf oc.tar && rm oc.tar && \
sudo mv oc /usr/local/bin/

# Verify successfully installed oc version
oc version
```

More Information: <https://docs.openshift.com/container-platform/4.9/cli_reference/openshift_cli/getting-started-cli.html>

#### 10. Provision Jenkins Agent with Node.js `16.x`

It might happen that your `ODS@4.x` setup only provides a Jenkins agent with Node.js `12.x`. However, in order to be able to work with the latest version and to have potential security holes closed, a Jenkins agent with the latest Node.js version is required for the build process in the CI/CD process.

<details><summary>How do I find out which a Jenkins Agent with Node.js are available in my <code>ODS@4.x</code> setup?</summary>

Go to <https://oauth-openshift.apps.OPENSHIFT_DOMAIN_DEV/k8s/ns/ods/build.openshift.io~v1~BuildConfig?name=jenkins-agent-nodejs>

</details>

In case it does not exist yet, it can be easily created with the following commands:

<details><summary>How to find the <code>oc</code> login token</summary>

1. Go to <https://oauth-openshift.apps.OPENSHIFT_DOMAIN_DEV/oauth/token/display>
2. Click on `Display token` or `Request another token`

</details>

```sh
# Login to OpenShift dev instance
oc login --server=https://api.OPENSHIFT_DOMAIN_DEV:6443 --token=123...456

# Switch project
oc project foo-cd

# Provision jenkins-agent-nodejs-16
oc process -f https://raw.githubusercontent.com/SimonGolms/ods-jenkins-agent-nodejs/main/jenkins-agent-nodejs-16-template.yaml | oc create -f -
```

For more information about the Jenkins agent, see: <https://github.com/SimonGolms/ods-jenkins-agent-nodejs>

#### 11. Setup Bitbucket Code Repository

1. Create BitBucket Repository

   - Replace `USER@COMPANY.COM` with an authorized (administrative) user with access to the Bitbucket project

   ```sh
   # For security reasons (e.g. terminal history) --user 'USERNAME:PASSWORD' should be avoided.
   # Instead, a prompt will show up for the password if --user 'USERNAME' is used!
   curl --data '{"defaultBranch":"master","description":"📱 Repo of the app from foo build with ionic and react","name":"foo-app"}' \
     --header "Content-Type: application/json" \
     --request POST \
     --url https://BITBUCKET_DOMAIN/rest/api/1.0/projects/foo/repos/ \
     --user USER@COMPANY.COM
   ```

2. Get trigger secret from the webhook proxy

   ```sh
   # Login to OpenShift dev instance
   oc login --server=https://api.OPENSHIFT_DOMAIN_DEV:6443 --token=123...456

   # Get trigger secret 'webhook-proxy' in plaintext
   oc get secret webhook-proxy --namespace foo-cd --output jsonpath='{.data.trigger-secret}' | base64 -d | xargs
   ```

3. Create Webhook

   - Replace `TRIGGER_SECRET` with the obtained trigger secret from previous step.
   - Replace `USER@COMPANY.COM` with an authorized (administrative) user with access to the Bitbucket project

   ```sh
   # For security reasons (e.g. terminal history) --user 'USERNAME:PASSWORD' should be avoided.
   # Instead, a prompt will show up for the password if --user 'USERNAME' is used!
   curl --data '{"active":true,"configuration":{},"events":["pr:merged","repo:refs_changed","pr:declined","pr:deleted"],"name":"Jenkins","url":"https://webhook-proxy-foo-cd.apps.OPENSHIFT_DOMAIN_DEV?trigger_secret=TRIGGER_SECRET"}' \
     --header "Content-Type: application/json" \
     --request POST \
     --url https://BITBUCKET_DOMAIN/rest/api/1.0/projects/foo/repos/foo-app/webhooks \
     --user USER@COMPANY.COM
   ```

4. Publish to Bitbucket Code Repository

   ```sh
   # Requires git v2.31.1
   git init --initial-branch=master
   git add --all
   git commit -m "chore: initial version"
   git remote add origin https://BITBUCKET_DOMAIN/scm/foo/foo-app.git
   # Before you push your first commit, make sure that no credentials are in the README as a result of the previous steps.
   # You might also delete unnecessary content in this context, like the 'Provision Quickstarter' section of this README.
   git push -u origin HEAD:master
   ```

### Verify successfully provision

If the provisioning was successful, the previous push of the first commit should have triggered the first build process in Jenkins in the meantime, which can be viewed under the following link: <https://jenkins-foo-cd.apps.OPENSHIFT_DOMAIN_DEV/job/foo-cd/job/foo-cd-app-master/>

#### Feature Environment

A new feature environment is created by the associated git branch name, e.g. `feature/next`.

```sh
# Creates and switch to new branch from the current branch
git checkout -b feature/next

# Add empty commit in case the previous commit includes '[skip ci]'
git commit -m "chore: create feature-next environment" --allow-empty

# Push the new branch to the remote repository
git push -u origin feature/next
```

A new Jenkins build should have been created and can be followed under the following link: <https://jenkins-foo-cd.apps.OPENSHIFT_DOMAIN_DEV/job/foo-cd/job/foo-cd-app-feature-next/>

Assuming the Jenkins build has been successfully completed, the application should have been created in the OpenShift 4 project [`foo-dev`](https://console-openshift-console.apps.OPENSHIFT_DOMAIN_DEV/topology/ns/foo-dev) as a new [`HelmRelease`](https://console-openshift-console.apps.OPENSHIFT_DOMAIN_DEV/helm-releases/ns/foo-dev/release/foo-app-feature-next) resource and should be accessible under the following link: <https://foo-app-feature-next.apps.OPENSHIFT_DOMAIN_DEV>

#### Release to `dev`, `test` and `prod`

1. Update your `metadata.yml` in your release manager repository

   ```yaml
   # Example metadata.yml
   id: foo
   name: Project foo
   description: Description of foo

   environments:
     prod:
       apiUrl: api.OPENSHIFT_DOMAIN_PROD:6443
       credentialsId: foo-cd-foo-prod

   repositories:
     - id: app
       branch: master
       url: https://bitbucket.biscrum.com/scm/foo/foo-app.git

   services:
     bitbucket:
       credentials:
         id: foo-cd-cd-user-with-password
     # jira:
     #   credentials:
     #     id: foo-cd-cd-user-with-password
     nexus:
       repository:
         name: leva-documentation
   ```

2. Go to the Jenkins build of the release manager and start a new build process in the `dev` environment. Assuming the release has been successfully completed, the application should have been created in the OpenShift 4 project [`foo-dev`](https://console-openshift-console.apps.OPENSHIFT_DOMAIN_DEV/topology/ns/foo-dev) as a new [`HelmRelease`](https://console-openshift-console.apps.OPENSHIFT_DOMAIN_DEV/helm-releases/ns/foo-dev/release/app) resource and should be accessible under the following link: <https://foo-app-dev.apps.OPENSHIFT_DOMAIN_DEV>

3. Before you can deploy a release into `qa`/`test` environment, you need to merge the release branch into your master branch to pass the checks in the Jenkins shared library stage [`odsOrchestrationPipeline`](https://github.com/opendevstack/ods-jenkins-shared-library/blob/4.x/vars/odsOrchestrationPipeline.groovy), see comment in [`metadata.yml`](./metadata.yml) for more details:

   ```sh
   # Switch to master branch
   git checkout master

   # Merge the remote release branch into master without opening a text editor and accept the auto-generated message
   git merge origin/release/<VERSION> --no-edit

   # Push the changes to the remote repository
   git push
   ```

4. Go to the Jenkins build of the release manager and start a new build process in the `qa`/`test` environment. Assuming the release has been successfully completed, the application should have been created in the OpenShift 4 project [`foo-test`](https://console-openshift-console.apps.OPENSHIFT_DOMAIN_DEV/topology/ns/foo-test) as a new [`HelmRelease`](https://console-openshift-console.apps.OPENSHIFT_DOMAIN_DEV/helm-releases/ns/foo-test/release/app) resource and should be accessible under the following link: <https://foo-app-test.apps.OPENSHIFT_DOMAIN_DEV>

5. Go to the Jenkins build of the release manager and start a new build process in the `prod` environment. Assuming the release has been successfully completed, the application should have been created in the OpenShift 4 project [`foo-prod`](https://console-openshift-console.apps.OPENSHIFT_DOMAIN_PROD/topology/ns/foo-prod) as a new [`HelmRelease`](https://console-openshift-console.apps.OPENSHIFT_DOMAIN_PROD/helm-releases/ns/foo-prod/release/app) resource and should be accessible under the following link: <https://foo-app.apps.OPENSHIFT_DOMAIN_DEV>

---

## Technology Stack

### Programming Language

[![TypeScript](https://img.shields.io/badge/typescript-3178C6.svg?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![JavaScript](https://img.shields.io/badge/javascript-F7DF1E.svg?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![HTML](https://img.shields.io/badge/html5-E34F26.svg?style=for-the-badge&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/css3-1572B6.svg?style=for-the-badge&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![npm](https://img.shields.io/badge/npm-CB3837.svg?style=for-the-badge&logo=npm&logoColor=white)](https://www.npmjs.com/)
[![Node.JS](https://img.shields.io/badge/node.js-339933.svg?style=for-the-badge&logo=nodedotjs&logoColor=white)](https://nodejs.org/)
[![Markdown](https://img.shields.io/badge/markdown-000000.svg?style=for-the-badge&logo=markdown&logoColor=white)](https://daringfireball.net/projects/markdown/)

### Frameworks and libraries

[![Ionic](https://img.shields.io/badge/ionic-3880FF.svg?style=for-the-badge&logo=ionic&logoColor=white)](https://ionicframework.com/)
[![React](https://img.shields.io/badge/react-20232a.svg?style=for-the-badge&logo=react&logoColor=61DAFB)](https://reactjs.org/)
[![React Router](https://img.shields.io/badge/React%20Router-CA4245.svg?style=for-the-badge&logo=react-router&logoColor=white)](https://reactjs.org/)
[![Redux Toolkit](https://img.shields.io/badge/Redux%20Toolkit-593d88.svg?style=for-the-badge&logo=redux&logoColor=white)](https://redux-toolkit.js.org/)
[![RTK Query](https://img.shields.io/badge/RTK%20Query-593d88.svg?style=for-the-badge&logo=redux&logoColor=white)](https://redux-toolkit.js.org/rtk-query/overview)
[![Azure](https://img.shields.io/badge/Azure%20SSO-0078D4.svg?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-react)
[![msal-react](https://img.shields.io/badge/MSAL%20React-5E5E5E.svg?style=for-the-badge&logo=microsoft&logoColor=white)](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-react)

**Testing**:

[![React Testing Library](https://img.shields.io/badge/React--Testing--Library-E33332.svg?style=for-the-badge&logo=testing-library&logoColor=white)](https://testing-library.com/docs/react-testing-library/intro)
[![Jest](https://img.shields.io/badge/Jest-C21325.svg?style=for-the-badge&logo=jest&logoColor=white)](https://jestjs.io/docs/getting-started)

**Tracking**:

N/A

**Linter**:

[![ESLint](https://img.shields.io/badge/ESlint-4B32C3.svg?style=for-the-badge&logo=eslint&logoColor=white)](https://eslint.org/)
[![Stylelint](https://img.shields.io/badge/stylelint-263238.svg?style=for-the-badge&logo=stylelint&logoColor=white)](https://stylelint.io/)
[![Prettier](https://img.shields.io/badge/Prettier-F7B93E.svg?style=for-the-badge&logo=prettier&logoColor=black)](https://prettier.io/)
[![Commitlint](https://img.shields.io/badge/commitlint-121212.svg?style=for-the-badge&&logoColor=black)](https://commitlint.js.org/)

**Compiler**:

[![react-scripts](<https://img.shields.io/badge/react--scripts%20(CRA)-20232a.svg?style=for-the-badge&logo=react&logoColor=61DAFB>)](https://create-react-app.dev/)

### CI/CD

[![OpenDevStack](https://img.shields.io/badge/OpenDevStack-222.svg?style=for-the-badge&logoColor=white)](https://www.opendevstack.org/)
[![Jenkins](https://img.shields.io/badge/Jenkins-D24939.svg?style=for-the-badge&logo=jenkins&logoColor=white)](https://nginx.org/)
[![Helm](https://img.shields.io/badge/Helm-0F1689.svg?style=for-the-badge&logo=helm&logoColor=white)](https://helm.sh/)
[![Semantic Release](https://img.shields.io/badge/Semantic%20Release-494949.svg?style=for-the-badge&logo=semantic-release&logoColor=white)](https://semantic-release.gitbook.io/semantic-release/)
[![Husky](https://img.shields.io/badge/%F0%9F%90%B6%20Husky-42b983.svg?style=for-the-badge)](https://typicode.github.io/husky/#/)

### Hosting

[![RedHat OpenShift v4.11](https://img.shields.io/badge/RedHat%20OpenShift-EE0000.svg?style=for-the-badge&logo=red-hat-open-shift&logoColor=white)](https://docs.openshift.com/container-platform/4.10/welcome/index.html)
[![Docker](https://img.shields.io/badge/Docker-2496ED.svg?style=for-the-badge&logo=docker&logoColor=white)](https://docs.docker.com/)
[![Nginx](https://img.shields.io/badge/Nginx-009639.svg?style=for-the-badge&logo=nginx&logoColor=white)](https://nginx.org/)

### Dev Environment

[![WSL2](https://img.shields.io/badge/Windows%20Subsystem%20for%20Linux%20%28WSL2%29-4D4D4D.svg?style=for-the-badge&logo=windows-terminal&logoColor=white)](https://docs.microsoft.com/en-us/windows/wsl/)

**IDEs/Editors**:

[![Visual Studio Code](https://img.shields.io/badge/Visual%20Studio%20Code-0078d7.svg?style=for-the-badge&logo=visual-studio-code&logoColor=white)](https://code.visualstudio.com/)

### Version Control

[![Git](https://img.shields.io/badge/git-F05033.svg?style=for-the-badge&logo=git&logoColor=white)](https://git-scm.com/doc)
[![Bitbucket](https://img.shields.io/badge/bitbucket-0047B3.svg?style=for-the-badge&logo=bitbucket&logoColor=white)](https://bitbucket.org/)

### Social

[![MS Teams](https://img.shields.io/badge/microsoft%20teams-6264a7.svg?style=for-the-badge&logo=microsoft-teams&logoColor=white)](https://www.microsoft.com/en-us/microsoft-teams/)

---

## Prerequisites

1. **Azure App Registration**

   Make sure you have an existing Azure App registry that has a single-page application (SPA) redirect to `http://localhost/`.

   Ideally you have one Azure App registry per environment (`dev`/`test`/`prod`) with at least the following SPA redirects:

   - Dev: `http://localhost/`, `https://foo-app-dev.apps.OPENSHIFT_DOMAIN_DEV`
   - Test: `http://localhost/`, `https://foo-app-test.apps.OPENSHIFT_DOMAIN_DEV`
   - Prod: `http://localhost/`, `https://foo-app.apps.OPENSHIFT_DOMAIN_PROD`

   Update the following entries with the `Application (client) ID` and `Directory (tenant) ID` from the corresponding app registry environment

   1. [`.env`](./.env)

      ```diff
      # Azure - SSO
      - REACT_APP_AZURE_ACTIVE_DIRECTORY_CLIENT_ID=""
      + REACT_APP_AZURE_ACTIVE_DIRECTORY_CLIENT_ID="123...789"
      - REACT_APP_AZURE_ACTIVE_DIRECTORY_TENANT_ID=""
      + REACT_APP_AZURE_ACTIVE_DIRECTORY_TENANT_ID="123...789"
      ```

   2. [`./chart/values.dev.yaml`](./chart/values.dev.yaml)

      _Please make sure that you use the correct client id and tenant id from your app registration for the `dev` environment._

      ```diff
      - azureActiveDirectoryClientId: "11111111-2222-3333-4444-555555555555"
      + azureActiveDirectoryClientId: "123...-dev-...789"
      - azureActiveDirectoryTenantId: "aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
      + azureActiveDirectoryTenantId: "abc...-dev-...xyz"
      ```

   3. [`./chart/values.test.yaml`](./chart/values.test.yaml)

      _Please make sure that you use the correct client id and tenant id from your app registration for the `test` environment._

      ```diff
      - azureActiveDirectoryClientId: "11111111-2222-3333-4444-555555555555"
      + azureActiveDirectoryClientId: "123...-test-...789"
      - azureActiveDirectoryTenantId: "aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
      + azureActiveDirectoryTenantId: "abc...-test-...xyz"
      ```

   4. [`./chart/values.prod.yaml`](./chart/values.prod.yaml)

      _Please make sure that you use the correct client id and tenant id from your app registration for the `prod` environment._

      ```diff
      - azureActiveDirectoryClientId: "11111111-2222-3333-4444-555555555555"
      + azureActiveDirectoryClientId: "123...-prod-...789"
      - azureActiveDirectoryTenantId: "aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
      + azureActiveDirectoryTenantId: "abc...-prod-...xyz"
      ```

   More information: <https://docs.microsoft.com/en-us/azure/active-directory/develop/scenario-spa-app-registration>

## Local Development

### Requirements

- Helm v3+
- Node.js v16+
- NPM v8+
- oc v4.9+

#### Using [`NVM`](https://github.com/nvm-sh/nvm)

```sh
# Install latest LTS Version (v16+) with the latest npm version (v8+)
nvm install --lts --latest-npm
```

### Set Environment Variables

See `.env.template` to create appropriate `.env` file. Ask your colleagues which values are currently necessary!

### Install Dependencies

```sh
npm install
```

### Start Development Server

```sh
npm run start
```

Starts the development server and makes your application accessible at `localhost:8100`. Changes in the application code will be hot-reloaded.

### Create Production Build (Web)

```sh
npm run build
```

The app is built for optimal performance: assets are minified and served gzipped.

### Run tests

```sh
npm run test
```

### Docker

#### Create Docker Image

```sh
npm run build
mv build docker
docker build -t foo-app -f docker/Dockerfile docker
```

In case the command `RUN apk update && apk upgrade` cannot be executed (e.g. working behind a proxy), uncomment it for the moment.

#### Start Docker Image

```sh
docker run -p 8080:8080 --env-file .env foo-app
```

Starts the [nginx](https://nginx.org) server and makes your application accessible at `localhost:8080`.

## Continuous Integration/Continuous Delivery (CI/CD)

This CI/CD setup has been developed for the 'trunk-based development' approach.

> _[...] Trunk-based development is a version control management practice where developers merge small, frequent updates to a core “trunk” or main branch. [...] Trunk-based development is far more simplified since it focuses on the main branch as the source of fixes and releases. In trunk-based development the main branch is assumed to always be stable, without issues, and ready to deploy [...]._ - <https://www.atlassian.com/continuous-delivery/continuous-integration/trunk-based-development>

### Master Branch

The `master` branch is your only real **source-of-true** 📜 and should always reflect the state as found in all three environments.

It is recommended not to merge any changes into the `master`-branch before a new release is triggered. Otherwise there is the risk of not being able to perform a hotfix immediately. The only solution remains a corresponding Git Strategy to restore the old state, import the necessary hotfix changes, release and then add the reset changes again.

With each commit, the source code in the master branch is checked for its releasability and tagged at the end with a new semantic version based on the git commit history.

```mermaid
%% If the Mermaid Diagram is not rendered (as is the case on BitBucket), it can be viewed at https://mermaid.live/
flowchart TB
    subgraph openshift-dev["OpenShift (DEV)"]
        subgraph ods
            subgraph sonarqube["SonarQube"]
                direction TB
                ods-DC-sonarqube["sonarqube (DeploymentConfig)"]:::classDeploymentConfig <-. Port 9000 .-> ods-S-sonarqube["sonarqube (Service)"]:::classService <-. Port 9000 .-> ods-RT-sonarqube["sonarqube (Route)\nhttps://sonarqube-ods.apps.OPENSHIFT_DOMAIN_DEV"]:::classRoute
            end
        end
        subgraph aqua
            aqua-aqua["Aqua Container Security"]
        end
        subgraph foo-cd
            subgraph webhook-proxy
                direction TB
                cd-DC-webhook-proxy["webhook-proxy (DeploymentConfig)"]:::classDeploymentConfig <-. Port 8080 .-> cd-S-webhook-proxy["webhook-proxy (Service)"]:::classService <-. Port 8080 .-> cd-RT-webhook-proxy["webhook-proxy (Route)\nhttps://webhook-proxy-foo-cd.apps.OPENSHIFT_DOMAIN_DEV"]:::classRoute
            end
            subgraph Jenkins
                subgraph Jenkinsfile
                    stageInitialize-->stageInstallDependency-->stageVersioning-->stageWorkaroundFindOpenShiftImageOrElse --> stageAnalyzeCode-->odsComponentStageScanWithSonar-->stageBuild-->stageDeploy-->odsComponentStageBuildOpenShiftImage-->stageWorkaroundUnitTest-->stageWorkaroundRolloutDeployment-->stageRelease
                end
            end
            subgraph cd-IS-foo-app-master["foo-app-master (Image Stream)"]
                cd-IST-foo-app-master["foo-app-master:v1.4.2"]:::classImageStreamTag
            end
        end
    end
    subgraph BitBucket
        subgraph bb-project-foo["foo (Project)"]
            subgraph bb-project-foo-app["foo-app (Repo)"]
                bb-project-foo-app-branch-master["master (Branch)"]
            end
        end
    end


aqua-aqua -- scan --> cd-IST-foo-app-master
bb-project-foo-app -- trigger --> webhook-proxy -- trigger --> Jenkins
bb-project-foo-app-branch-master -- pull --> Jenkinsfile
odsComponentStageBuildOpenShiftImage -- push --> cd-IST-foo-app-master
odsComponentStageBuildOpenShiftImage -. trigger .-> aqua-aqua -. result .-> odsComponentStageBuildOpenShiftImage
odsComponentStageScanWithSonar -. trigger .-> sonarqube -. result .-> odsComponentStageScanWithSonar
stageRelease -- "push (v1.4.2)" --> bb-project-foo-app-branch-master

%% stlyes
classDef classBitBucket fill:#2684FF22,stroke:#2684FF,stroke-width:4px
classDef classBitBucketProject fill:#2684FF22,stroke:#2684FF
classDef classBuildConfig fill:#00408022,stroke:#004080
classDef classDeployment fill:#00408022,stroke:#004080
classDef classDeploymentConfig fill:#00408022,stroke:#004080
classDef classHelmRelease fill:#2b9af322,stroke:#2b9af3
classDef classImageStream fill:#2b9af322,stroke:#2b9af3
classDef classImageStreamTag fill:#2b9af322,stroke:#2b9af3
classDef classOcpProject fill:#ffffff00,stroke:#f00,stroke-width:2px
classDef classOcpResource fill:#ffffff00,stroke:#06c,stroke-width:2px
classDef classOpenShift fill:#ffffff00,stroke:#f00,stroke-width:4px
classDef classRoute fill:#2b9af322,stroke:#2b9af3
classDef classService fill:#6ca10022,stroke:#6ca100

class BitBucket classBitBucket
class bb-project-foo,bb-project-foo-app classBitBucketProject
class cd-IS-foo-app-master classImageStream
class aqua,ods,foo-cd,foo-dev classOcpProject
class aqua-aqua,Jenkins,Jenkinsfile,sonarqube,webhook-proxy classOcpResource
class openshift-dev classOpenShift
```

### Feature Environments

With each new `feature/*` branch created, a new environment is created in the OpenShift Project `foo-cd`.
Different stages are processed in the Jenkinsfile and finally rolled out and managed via Helm.

Please be aware that a new route (e.g. <https://foo-app-feature-next.apps.OPENSHIFT_DOMAIN_DEV>) is created for each new feature environment. If this is required for the SSO login, it must be specified as a new valid redirect URL in the app registration.

```mermaid
%% If the Mermaid Diagram is not rendered (as is the case on BitBucket), it can be viewed at https://mermaid.live/
flowchart TB
    subgraph openshift-dev["OpenShift (DEV)"]
        subgraph ods
            subgraph sonarqube["SonarQube"]
                direction TB
                ods-DC-sonarqube["sonarqube (DeploymentConfig)"]:::classDeploymentConfig <-. Port 9000 .-> ods-S-sonarqube["sonarqube (Service)"]:::classService <-. Port 9000 .-> ods-RT-sonarqube["sonarqube (Route)\nhttps://sonarqube-ods.apps.OPENSHIFT_DOMAIN_DEV"]:::classRoute
            end
        end
        subgraph foo-cd
            subgraph webhook-proxy
                direction TB
                cd-DC-webhook-proxy["webhook-proxy (DeploymentConfig)"]:::classDeploymentConfig <-. Port 8080 .-> cd-S-webhook-proxy["webhook-proxy (Service)"]:::classService <-. Port 8080 .-> cd-RT-webhook-proxy["webhook-proxy (Route)\nhttps://webhook-proxy-foo-cd.apps.OPENSHIFT_DOMAIN_DEV"]:::classRoute
            end
            subgraph Jenkins
                subgraph Jenkinsfile
                    stageInitialize-->stageInstallDependency-->stageVersioning-->stageWorkaroundFindOpenShiftImageOrElse -->|orElse| stageAnalyzeCode-->odsComponentStageScanWithSonar-->stageBuild-->stageDeploy-->odsComponentStageBuildOpenShiftImage-->stageWorkaroundUnitTest-->stageWorkaroundRolloutDeployment-->stageRelease
                end
            end
            subgraph cd-IS-foo-app-feature-next["foo-app-feature-next (Image Stream)"]
                cd-IST-foo-app-feature-next["foo-app-feature-next:hash"]:::classImageStreamTag
            end
        end
        subgraph foo-dev
            subgraph dev-HR-foo-app-feature-next["foo-app-feature-next (Helm Release)"]
                dev-D-app["app (Deployment)"]:::classDeployment <-. Port 8080 .-> dev-S-app["app (Service)"]:::classService <-. Port 8080 .-> dev-RT-app["app (Route)\nhttps://foo-app-feature-next.apps.OPENSHIFT_DOMAIN_DEV"]:::classRoute
            end
        end
    end
    subgraph bitbucket["BitBucket"]
        subgraph bitbucket-foo["foo (Project)"]
            subgraph bitbucket-foo-app["foo-app (Repo)"]
                bitbucket-foo-app-branch-feature-next["feature-next (Branch)"]
            end
        end
    end

bitbucket-foo-app -- trigger --> webhook-proxy -- trigger --> Jenkins
bitbucket-foo-app-branch-feature-next -- pull --> Jenkinsfile
cd-IST-foo-app-feature-next --> dev-D-app
odsComponentStageBuildOpenShiftImage -- push --> cd-IST-foo-app-feature-next
odsComponentStageScanWithSonar <-.-> sonarqube
stageWorkaroundRolloutDeployment -- stageRolloutWithHelm --> dev-HR-foo-app-feature-next

%% stlyes
classDef classBitBucket fill:#2684FF22,stroke:#2684FF,stroke-width:4px
classDef classBitBucketProject fill:#2684FF22,stroke:#2684FF
classDef classBuildConfig fill:#00408022,stroke:#004080
classDef classDeployment fill:#00408022,stroke:#004080
classDef classDeploymentConfig fill:#00408022,stroke:#004080
classDef classHelmRelease fill:#2b9af322,stroke:#2b9af3
classDef classImageStream fill:#2b9af322,stroke:#2b9af3
classDef classImageStreamTag fill:#2b9af322,stroke:#2b9af3
classDef classOcpProject fill:#ffffff00,stroke:#f00,stroke-width:2px
classDef classOcpResource fill:#ffffff00,stroke:#06c,stroke-width:2px
classDef classOpenShift fill:#ffffff00,stroke:#f00,stroke-width:4px
classDef classRoute fill:#2b9af322,stroke:#2b9af3
classDef classService fill:#6ca10022,stroke:#6ca100

class BitBucket classBitBucket
class bitbucket-foo,bitbucket-foo-app classBitBucketProject
class dev-HR-foo-app-feature-next classHelmRelease
class cd-IS-foo-app-feature-next classImageStream
class ods,foo-cd,foo-dev classOcpProject
class Jenkins,Jenkinsfile,sonarqube,webhook-proxy classOcpResource
class openshift-dev classOpenShift
```

### Release Manager

#### Release to `dev` environment

```mermaid
%% If the Mermaid Diagram is not rendered (as is the case on BitBucket), it can be viewed at https://mermaid.live/
flowchart TB
    subgraph openshift-dev["OpenShift (DEV)"]

        subgraph foo-cd
            subgraph jenkins["Jenkins"]
                subgraph jenkinsfile-foo-app["Jenkinsfile (foo-app)"]
                    stageInitialize-->stageInstallDependency-->stageVersioning-->stageWorkaroundFindOpenShiftImageOrElse --> stageAnalyzeCode-->odsComponentStageScanWithSonar-->stageBuild-->stageDeploy-->odsComponentStageBuildOpenShiftImage-->stageWorkaroundUnitTest-->stageWorkaroundRolloutDeployment-->stageRelease
                end
                build-with-parameters("<strong>Build with Parameters</strong>\nenvironment: dev\nversion: 20220518.001"):::classManualTask
                subgraph jenkinsfile-releasemanager["Jenkinsfile (Release Manager)"]
                    InitStage --> BuildStage --> DeployStage --> TestStage --> ReleaseStage --> FinalizeStage
                end
            end
            subgraph cd-IS-app["app (Image Stream)"]
                cd-IST-app["app:20220518.001"]:::classImageStreamTag
            end
        end
        subgraph ods
            subgraph sonarqube["SonarQube"]
                direction TB
                ods-DC-sonarqube["sonarqube (DeploymentConfig)"]:::classDeploymentConfig <-. Port 9000 .-> ods-S-sonarqube["sonarqube (Service)"]:::classService <-. Port 9000 .-> ods-RT-sonarqube["sonarqube (Route)\nhttps://sonarqube-ods.apps.OPENSHIFT_DOMAIN_DEV"]:::classRoute
            end
        end
        subgraph aqua
            aqua-aqua["Aqua Container Security"]
        end
        subgraph foo-dev
            subgraph dev-HR-app["app (Helm Release)"]
                direction TB
                dev-D-app["app (Deployment)"]:::classDeployment <-. Port 8080 .-> dev-S-app["app (Service)"]:::classService <-. Port 8080 .-> dev-RT-app["app (Route)\nhttps://foo-dev.apps.OPENSHIFT_DOMAIN_DEV"]:::classRoute
            end
        end
    end
    subgraph BitBucket
        subgraph bitbucket-foo["foo (Project)"]
            subgraph bitbucket-foo-app["foo-app (Repo)"]
                bitbucket-foo-app-branch-master["master (Branch)"]
                bitbucket-foo-app-branch-release["release/20220518.001 (Branch)"]
            end
            subgraph bitbucket-foo-releasemanager["foo-releasemanager (Repo)"]
                bitbucket-foo-releasemanager-branch-master["master (Branch)"]
            end
        end
    end

aqua-aqua -- scan --> cd-IST-app
cd-IST-app --> dev-D-app
bitbucket-foo-app-branch-master -- pull --> jenkinsfile-foo-app
bitbucket-foo-releasemanager-branch-master -- pull --> jenkinsfile-releasemanager
BuildStage -- trigger --> jenkinsfile-foo-app
build-with-parameters -. trigger .-> InitStage
FinalizeStage -- push --> bitbucket-foo-app-branch-release
FinalizeStage -- push --> bitbucket-foo-releasemanager-branch-master
odsComponentStageBuildOpenShiftImage -- push --> cd-IST-app
odsComponentStageBuildOpenShiftImage -. trigger .-> aqua-aqua -. result .-> odsComponentStageBuildOpenShiftImage
odsComponentStageScanWithSonar -. trigger .-> sonarqube -. result .-> odsComponentStageScanWithSonar
stageWorkaroundRolloutDeployment -- "Rollout with Helm" --> dev-HR-app

%% stlyes
classDef classBitBucket fill:#2684FF22,stroke:#2684FF,stroke-width:4px
classDef classBitBucketProject fill:#2684FF22,stroke:#2684FF
classDef classBuildConfig fill:#00408022,stroke:#004080
classDef classDeployment fill:#00408022,stroke:#004080
classDef classDeploymentConfig fill:#00408022,stroke:#004080
classDef classHelmRelease fill:#2b9af322,stroke:#2b9af3
classDef classImageStream fill:#2b9af322,stroke:#2b9af3
classDef classImageStreamTag fill:#2b9af322,stroke:#2b9af3
classDef classOcpProject fill:#ffffff00,stroke:#f00,stroke-width:2px
classDef classOcpResource fill:#ffffff00,stroke:#06c,stroke-width:2px
classDef classOpenShift fill:#ffffff00,stroke:#f00,stroke-width:4px
classDef classRoute fill:#2b9af322,stroke:#2b9af3
classDef classService fill:#6ca10022,stroke:#6ca100
classDef classManualTask fill:#65bd1022,stroke:#65bd10,stroke-width:4px

class BitBucket classBitBucket
class bitbucket-foo,bitbucket-foo-app,bitbucket-foo-releasemanager classBitBucketProject
class dev-HR-app classHelmRelease
class cd-IS-app classImageStream
class aqua,ods,foo-cd,foo-dev classOcpProject
class aqua-aqua,jenkins,jenkinsfile-foo-app,jenkinsfile-releasemanager,sonarqube,webhook-proxy classOcpResource
class openshift-dev classOpenShift
```

#### Release to `test` environment

```mermaid
%% If the Mermaid Diagram is not rendered (as is the case on BitBucket), it can be viewed at https://mermaid.live/
flowchart TB
    subgraph openshift-dev["OpenShift (DEV)"]
        subgraph foo-cd
            subgraph jenkins["Jenkins"]
                build-with-parameters{{"<strong>Build with Parameters</strong>\nenvironment: qa\nversion: 20220518.001"}}:::classManualTask
                subgraph jenkinsfile-releasemanager["Jenkinsfile (Release Manager)"]
                    InitStage --> BuildStage --> DeployStage --> TestStage --> ReleaseStage --> FinalizeStage
                end
                subgraph jenkinsfile-foo-app["Jenkinsfile (foo-app)"]
                    stageInitialize --> stageInstallDependency --> stageVersioning --> stageWorkaroundFindOpenShiftImageOrElse --> stageWorkaroundUnitTest --> stageWorkaroundRolloutDeployment --> stageRelease
                end
            end
            subgraph cd-IS-app["app (Image Stream)"]
                cd-IST-app["app:20220518.001"]:::classImageStreamTag
            end
        end
        subgraph foo-test
            subgraph test-HR-app["app (Helm Release)"]
                test-D-app["app (Deployment)"]:::classDeployment <-. Port 8080 .-> test-S-app["app (Service)"]:::classService <-. Port 8080 .-> test-RT-app["app (Route)\nhttps://foo-test.apps.OPENSHIFT_DOMAIN_DEV"]:::classRoute
            end
        end
    end
    subgraph BitBucket
        subgraph bitbucket-foo["foo (Project)"]
            subgraph bitbucket-foo-app["foo-app (Repo)"]
                bitbucket-foo-app-branch-master["master (Branch)"]
                merge{{"<strong>Merge into master</strong>\nrelease/20220518.001 (Branch)"}}:::classManualTask
            end
            subgraph bitbucket-foo-releasemanager["foo-releasemanager (Repo)"]
                bitbucket-foo-releasemanager-branch-master["master (Branch)"]
            end
        end
    end

cd-IST-app <-.-> stageWorkaroundFindOpenShiftImageOrElse
cd-IST-app --> test-D-app
bitbucket-foo-app-branch-master -- pull --> jenkinsfile-foo-app
bitbucket-foo-releasemanager-branch-master -- pull --> jenkinsfile-releasemanager
merge --> bitbucket-foo-app-branch-master["master (Branch)"]
BuildStage -- trigger --> jenkinsfile-foo-app
build-with-parameters -. trigger .-> InitStage
FinalizeStage -- push --> bitbucket-foo-releasemanager-branch-master
stageWorkaroundRolloutDeployment -- "Rollout with Helm" --> test-HR-app

%% stlyes
classDef classBitBucket fill:#2684FF22,stroke:#2684FF,stroke-width:4px
classDef classBitBucketProject fill:#2684FF22,stroke:#2684FF
classDef classBuildConfig fill:#00408022,stroke:#004080
classDef classDeployment fill:#00408022,stroke:#004080
classDef classDeploymentConfig fill:#00408022,stroke:#004080
classDef classHelmRelease fill:#2b9af322,stroke:#2b9af3
classDef classImageStream fill:#2b9af322,stroke:#2b9af3
classDef classImageStreamTag fill:#2b9af322,stroke:#2b9af3
classDef classOcpProject fill:#ffffff00,stroke:#f00,stroke-width:2px
classDef classOcpResource fill:#ffffff00,stroke:#06c,stroke-width:2px
classDef classOpenShift fill:#ffffff00,stroke:#f00,stroke-width:4px
classDef classRoute fill:#2b9af322,stroke:#2b9af3
classDef classService fill:#6ca10022,stroke:#6ca100
classDef classManualTask fill:#65bd1022,stroke:#65bd10,stroke-width:4px

class BitBucket classBitBucket
class bitbucket-foo,bitbucket-foo-app,bitbucket-foo-releasemanager classBitBucketProject
class test-HR-app classHelmRelease
class cd-IS-app classImageStream
class aqua,ods,foo-cd,foo-test classOcpProject
class aqua-aqua,jenkins,jenkinsfile-foo-app,jenkinsfile-releasemanager,sonarqube,webhook-proxy classOcpResource
class openshift-dev classOpenShift
```

#### Release to `prod` environment

```mermaid
%% If the Mermaid Diagram is not rendered (as is the case on BitBucket), it can be viewed at https://mermaid.live/
flowchart TB
    subgraph openshift-dev["OpenShift (DEV)"]
        subgraph foo-cd
            subgraph jenkins["Jenkins"]
                build-with-parameters{{"<strong>Build with Parameters</strong>\nenvironment: prod\nversion: 20220518.001"}}:::classManualTask
                subgraph jenkinsfile-releasemanager["Jenkinsfile (Release Manager)"]
                    InitStage --> BuildStage --> DeployStage --> TestStage --> ReleaseStage --> FinalizeStage
                end
                subgraph jenkinsfile-foo-app["Jenkinsfile (foo-app)"]
                    stageInitialize --> stageInstallDependency --> stageVersioning --> stageWorkaroundFindOpenShiftImageOrElse --> stageWorkaroundUnitTest --> stageWorkaroundRolloutDeployment --> stageRelease
                end
            end
            subgraph cd-IS-app["app (Image Stream)"]
                cd-IST-app["app:20220518.001"]:::classImageStreamTag
            end
        end
    end
    subgraph openshift-prod["OpenShift (PROD)"]
        subgraph foo-prod
            subgraph prod-HR-app["app (Helm Release)"]
                prod-D-app["app (Deployment)"]:::classDeployment <-. Port 8080 .-> prod-S-app["app (Service)"]:::classService <-. Port 8080 .-> prod-RT-app["app (Route)\nhttps://foo.apps.OPENSHIFT_DOMAIN_PROD"]:::classRoute
            end
        end
    end
    subgraph BitBucket
        subgraph bitbucket-foo["foo (Project)"]
            subgraph bitbucket-foo-app["foo-app (Repo)"]
                bitbucket-foo-app-branch-master["master (Branch)"]
            end
            subgraph bitbucket-foo-releasemanager["foo-releasemanager (Repo)"]
                bitbucket-foo-releasemanager-branch-master["master (Branch)"]
            end
        end
    end

cd-IST-app --> prod-D-app
cd-IST-app <-.-> stageWorkaroundFindOpenShiftImageOrElse
bitbucket-foo-app-branch-master -- pull --> jenkinsfile-foo-app
bitbucket-foo-releasemanager-branch-master -- pull --> jenkinsfile-releasemanager
BuildStage -- trigger --> jenkinsfile-foo-app
build-with-parameters -. trigger .-> InitStage
FinalizeStage -- push --> bitbucket-foo-releasemanager-branch-master
stageWorkaroundRolloutDeployment -- "Rollout with Helm" --> prod-HR-app

%% stlyes
classDef classBitBucket fill:#2684FF22,stroke:#2684FF,stroke-width:4px
classDef classBitBucketProject fill:#2684FF22,stroke:#2684FF
classDef classBuildConfig fill:#00408022,stroke:#004080
classDef classDeployment fill:#00408022,stroke:#004080
classDef classDeploymentConfig fill:#00408022,stroke:#004080
classDef classHelmRelease fill:#2b9af322,stroke:#2b9af3
classDef classImageStream fill:#2b9af322,stroke:#2b9af3
classDef classImageStreamTag fill:#2b9af322,stroke:#2b9af3
classDef classOcpProject fill:#ffffff00,stroke:#f00,stroke-width:2px
classDef classOcpResource fill:#ffffff00,stroke:#06c,stroke-width:2px
classDef classOpenShift fill:#ffffff00,stroke:#f00,stroke-width:4px
classDef classRoute fill:#2b9af322,stroke:#2b9af3
classDef classService fill:#6ca10022,stroke:#6ca100
classDef classManualTask fill:#65bd1022,stroke:#65bd10,stroke-width:4px

class BitBucket classBitBucket
class bitbucket-foo,bitbucket-foo-app,bitbucket-foo-releasemanager classBitBucketProject
class prod-HR-app classHelmRelease
class cd-IS-app classImageStream
class aqua,ods,foo-cd,foo-prod classOcpProject
class aqua-aqua,jenkins,jenkinsfile-foo-app,jenkinsfile-releasemanager,sonarqube,webhook-proxy classOcpResource
class openshift-dev,openshift-prod classOpenShift
```

## Housekeeping

💡 From time to time, obsolete resources should be cleaned up. It would be best to have this automated at a later time.

### Git Branches

```sh
git checkout master

# Cleaning outdated branches
git fetch --prune

# Delete all local branches except current branch (e.g. master)
git branch | grep --invert-match '^*' | xargs git branch -D

# Delete all remote branches except master (may take some time)
# Skip git hooks with '--no-verify'
git branch -r | grep 'origin' | grep --invert-match 'master$' | grep --invert-match HEAD | cut -d/ -f2- | while read line; do git push --no-verify origin :heads/$line; done;
```

### Git Tags

```sh
# Delete all local tags that do NOT match a pattern of a semantic version
git tag -l | grep --invert-match '^v[[:digit:]].[[:digit:]].[[:digit:]]' | xargs git tag -d

# Delete all remote tags that do NOT match a pattern of a semantic version (e.g. ods-generated-v20220518.001)
# Skip git hooks with '--no-verify'
git ls-remote --tags origin | cut -d/ -f3- | grep --invert-match '^v[[:digit:]].[[:digit:]].[[:digit:]]' | grep -v '}$'| xargs git push --delete --no-verify origin
```

### OpenShift

#### Feature Environments

With the approach of making each feature available as a new deployed environment for testing before it is merged into the master branch, a number of environments are created in OpenShift over time. The easiest way to delete these is to use the following command:

```sh
# Login
oc login --server=https://api.OPENSHIFT_DOMAIN_DEV:6443 --token=123...456

# Switch to Project
oc project foo-dev

# Delete/Uninstall all feature charts
helm list | grep -e 'app' | cut -f1 | xargs helm uninstall

# Delete all other feature resources
oc get all --output jsonpath='{range .items[*]}{"oc delete "}{.kind}{" "}{.metadata.name}{" "}{"\n"}{end}' | grep -- "app-feature-" | while read -r line; do eval $line; done
```

#### Jenkins Pipelines

**Feature Pipelines**: Since OpenShift 4, Jenkins pipelines are treated as `BuildConfig`. Unfortunately, with `ODS@4.x` in the Jenkins stage [`odsComponentStageBuildOpenShiftImage`](https://www.opendevstack.org/ods-documentation/opendevstack/4.x/jenkins-shared-library/component-pipeline.html#_odscomponentstagebuildopenshiftimage), all builds are also created as a `BuildConfig` in the `cd` project without any further information filled labels. A distinction is not obvious at first view, but can be figured out via the configuration parameter `.spec.strategy.type` (`JenkinsPipeline` vs `Docker`).

**Release Pipelines**: Can be deleted without any problems, since they do not create any further resources, instead they are directly cancelled due to `[skip ci]` in the commit message.

**ODS Quickstarter**: Can be deleted after successful creation without any problems, as there is no further need for them and they only take up resources unnecessarily.

```sh
# Login
oc login --server=https://api.OPENSHIFT_DOMAIN_DEV:6443 --token=123...456

# Switch Project
oc project foo-cd

# Delete all feature pipelines (may take some time)
oc get bc --output jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.spec.strategy.type}{"\n"}{end}' | grep -e "JenkinsPipeline" | cut -f1 | grep -e "app-feature-" | while read -r line; do oc delete bc $line && sleep 10s; done

# Delete all release pipelines (may take some time)
oc get bc --output custom-columns=NAME:.metadata.name | grep -e "app-release-" | while read -r line; do oc delete bc $line && sleep 10s; done

# Delete all ods quickstarter pipelines (may take some time)
oc get bc --output custom-columns=NAME:.metadata.name | grep -e "ods-qs-" | while read -r line; do oc delete bc $line && sleep 10s; done
```

## Roadmap

- [x] Improve Documentation
- [ ] Implement Android
- [ ] Implement iOS
- [ ] Implement Ionic Appflow
- [ ] Improve Testing

## Author

**Simon Golms**

- Digital Card: `npx simongolms`
- Github: [@SimonGolms](https://github.com/SimonGolms)
- Website: [gol.ms](https://gol.ms)

## Contributing

Contributions, issues and feature requests are welcome!

## Show your support

Give a ⭐️ if this project helped you!

## License

Copyright © 2022 [Simon Golms](https://github.com/SimonGolms).<br />
This project is [Apache-2.0](https://github.com/SimonGolms/ods-quickstarter-fe-ionic-react/blob/master/LICENSE) licensed.

## Further Resources

- <https://docs.atlassian.com/bitbucket-server/rest/7.6.12/bitbucket-rest.html>
- <https://helm.sh/>
- <https://ionicframework.com>
- <https://reactjs.org>
- <https://www.opendevstack.org/>
