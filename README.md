## Amazon ECS "Render Task Definition" Action for GitHub Actions

Inserts a container image URI into an Amazon ECS task definition JSON file, creating a new task definition file.

## Usage

To insert the image URI `amazon/amazon-ecs-sample:latest` as the image for the `web` container in the task definition file, and then deploy the edited task definition file to ECS:

If you want to pass env vars to task container , you can add it to action env array with TASK_ prefix
An env var like  TASK_WP_LOGIN will be integrated as WP_LOGIN into container env

```yaml
    - name: Render Amazon ECS task definition
      id: render-web-container
      uses: aws-actions/amazon-ecs-render-task-definition@v1
      env:
        TASK_WP_LOGIN: bla
      with:
        task-definition: task-definition.json
        container-name: web
        image: amazon/amazon-ecs-sample:latest

    - name: Deploy to Amazon ECS service
      uses: aws-actions/amazon-ecs-deploy-task-definition@v1
      with:
        task-definition: ${{ steps.render-web-container.outputs.task-definition }}
        service: my-service
        cluster: my-cluster
```

## License Summary

This code is made available under the MIT license.
