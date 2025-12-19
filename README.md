name: Deploy to Server

on:
  push:
    branches:
      - main # Change to your default branch name if different

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v4 # Use the latest version of the checkout action

    - name: Deploy to Server
      uses: appleboy/ssh-action@v1.0.3 # A popular action for running SSH commands
      with:
        host: ${{ secrets.SERVER_IP }}
        username: ${{ secrets.SERVER_USER }}
        key: ${{ secrets.SSH_PRIVATE_KEY }}
        script: |
          cd ${{ secrets.APP_DIR }}
          git pull origin main # Pull the latest code
          # Add any post-deployment commands here, e.g.,
          # npm install
          # npm run build
          # systemctl restart your-service-name
