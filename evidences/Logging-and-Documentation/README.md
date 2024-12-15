[Deployment Process]
1. The code changes within the application are modified and committed, then pushed to the GitHub repository.
2. GitHub detects the changes and sends an event (push code) to trigger the Build Project in the CodeBuild service.
3. The Build Project is triggered and pulls the latest code from the linked GitHub repository, finds the buildspec.yml file, and executes the build commands specified in the file to package the application as a new image and push it to ECR.
4. The ECR now has the latest build of the code (with the build number). The coworking.yml file is then updated with the app's image, replacing it with the image tagged with the latest build number.
5. Run the command kubectl apply -f coworking.yml to update the app in the pod with the latest image.
6. Once the update process is complete, the app running in the coworking pod has been updated with the new changes.

[How Users Deploy Changes]
1. The user makes changes to the code, then commits and pushes the code to the GitHub repository.
2. Go to the ECR repository and find the image with the latest build number.
3. Update the app's image in the coworking.yml file with the image tag of the latest build number.
4.Run the command kubectl apply -f coworking.yml.