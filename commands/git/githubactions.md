A common pattern is:

Push code to GitHub.
A GitHub Actions workflow runs.
The workflow builds and tests your application.
It connects to your remote server over SSH.
It copies the new files or artifact.
It restarts your application (Docker, systemd, PM2, etc.).
Prerequisites

You'll need:

A GitHub repository.
A Linux server (Ubuntu/Debian/CentOS, etc.).
SSH access to the server.
A deployment user (avoid deploying as root if possible).
An SSH private key stored as a GitHub Secret.
Step 1: Generate an SSH key

On your local machine:

ssh-keygen -t ed25519 -C "github-actions"


This creates:

~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub


Copy the public key to your server:

ssh-copy-id deploy@your-server-ip


Or append it manually:

cat id_ed25519.pub >> ~/.ssh/authorized_keys


Test it:

ssh deploy@your-server-ip

Step 2: Add GitHub Secrets

Go to:

Repository → Settings → Secrets and variables → Actions

Create these secrets:

Secret	Example
HOST	192.168.1.100
USERNAME	deploy
SSH_KEY	Contents of id_ed25519 (private key)
PORT	22

Optional:

APP_PATH=/var/www/myapp

Step 3: Create the workflow

Create:

.github/workflows/deploy.yml


Example:

name: Deploy

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup SSH
        run: |
          mkdir -p ~/.ssh
          echo "${{ secrets.SSH_KEY }}" > ~/.ssh/id_ed25519
          chmod 600 ~/.ssh/id_ed25519
          ssh-keyscan -H ${{ secrets.HOST }} >> ~/.ssh/known_hosts

      - name: Deploy
        run: |
          ssh -i ~/.ssh/id_ed25519 \
          -p ${{ secrets.PORT }} \
          ${{ secrets.USERNAME }}@${{ secrets.HOST }} \
          "cd /var/www/myapp && git pull origin main"


When you push to main, the server will execute:

cd /var/www/myapp
git pull origin main

Option 2: Upload files using rsync

This is preferred if the server doesn't contain a Git repository.

name: Deploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Setup SSH
        run: |
          mkdir -p ~/.ssh
          echo "${{ secrets.SSH_KEY }}" > ~/.ssh/id_ed25519
          chmod 600 ~/.ssh/id_ed25519
          ssh-keyscan -H ${{ secrets.HOST }} >> ~/.ssh/known_hosts

      - name: Sync files
        run: |
          rsync -az --delete \
            -e "ssh -i ~/.ssh/id_ed25519 -p ${{ secrets.PORT }}" \
            ./ \
            ${{ secrets.USERNAME }}@${{ secrets.HOST }}:/var/www/myapp

Option 3: Build locally, deploy only build output

For example, a React application:

steps:
  - uses: actions/checkout@v4

  - uses: actions/setup-node@v4
    with:
      node-version: 22

  - run: npm ci

  - run: npm run build

  - name: Deploy build
    run: |
      rsync -az \
      -e "ssh -i ~/.ssh/id_ed25519" \
      build/ \
      deploy@server:/var/www/html/


Only the compiled files are uploaded.

Option 4: Deploy a Docker application

Build the image:

- run: docker build -t myapp .


On the server:

cd /opt/myapp
docker compose pull
docker compose up -d


Workflow:

- name: Restart Docker
  run: |
    ssh deploy@server "
      cd /opt/myapp &&
      git pull &&
      docker compose up -d --build
    "

Option 5: Restart a systemd service
- name: Restart service
  run: |
    ssh deploy@server "
      cd /var/www/myapp &&
      git pull &&
      sudo systemctl restart myapp &&
      sudo systemctl status myapp --no-pager
    "

Option 6: Restart a Node.js application with PM2
- name: Deploy
  run: |
    ssh deploy@server "
      cd /var/www/myapp &&
      git pull &&
      npm ci &&
      npm run build &&
      pm2 reload ecosystem.config.js
    "

Add build and test before deployment
steps:
  - uses: actions/checkout@v4

  - uses: actions/setup-node@v4
    with:
      node-version: 22

  - run: npm ci

  - run: npm test

  - run: npm run build

  - name: Deploy
    run: ssh ...


This prevents deployment if tests or the build fail.

Branch-specific deployments

Deploy production only from main:

on:
  push:
    branches:
      - main


Deploy staging:

on:
  push:
    branches:
      - develop

Best practices
Use GitHub Secrets for SSH keys, tokens, and passwords.
Use a dedicated deployment user with the minimum required permissions instead of root.
Pin GitHub Actions to specific major versions (or full commit SHAs for stricter security).
Run tests and build steps before deployment.
Use rsync --delete only if you're sure the destination should exactly mirror the repository.
Configure GitHub Environments (for example, staging and production) to require approvals before production deployments.
Example project structure
my-app/
├── .github/
│   └── workflows/
│       └── deploy.yml
├── src/
├── package.json
├── Dockerfile
└── docker-compose.yml


The exact deployment commands depend on your application's stack. If you tell me:

the language/framework (Node.js, Laravel, Django, Spring Boot, etc.),
whether you use Docker,
the operating system of the remote server, and
whether you want to git pull on the server or upload build artifacts,

I can provide a complete production-ready deploy.yml tailored to your setup.
