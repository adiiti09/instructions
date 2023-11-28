# Configuring github webhook and using it with Jenkins project

1. Go to github repo --> Settings -- Webhooks
2. Click Add webhook
3. In the Payload URL field enter http://<jenkins_server_hostname_or_ip>:<port>/github-webhook/ (replace your hostname or ip and port)
4. In the Content type fiels select application/json
5. Under Which events would you like to trigger this webhook? select as appropriate
6. Click Add Webhook
