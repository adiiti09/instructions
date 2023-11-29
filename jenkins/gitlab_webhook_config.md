# Gitlab webhook config process outline
1. Configure gitlab in Jenkins using gitlab API token for passwordless authentication. Manage Jenkins --> System Configuration --> System
2. Create a pipeline project and choose build trigger as Gitlab Webhook.
3. Copy the webhook URL shown in the project.
4. Also create a secret token under build trigger advanced settings.
5. Go to gitlab, to the specific project to be used in pipeline.
6. Under project settings, go to webhooks.
7. Create a webhook usin gthe webhook URL and secret token copied from jenkins.
8. Test the webhook using Test button.