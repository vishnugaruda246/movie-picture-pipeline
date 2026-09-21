# Movie Picture Pipeline — Submission

CI/CD pipelines for the Movie Picture frontend (React) and backend (Flask), built with GitHub Actions and deployed to Amazon EKS.

## Workflows

| Workflow | File | Trigger |
|---|---|---|
| Frontend Continuous Integration | `.github/workflows/frontend-ci.yaml` | Pull request to `main`, manual |
| Backend Continuous Integration | `.github/workflows/backend-ci.yaml` | Pull request to `main`, manual |
| Frontend Continuous Deployment | `.github/workflows/frontend-cd.yaml` | Push to `main`, manual |
| Backend Continuous Deployment | `.github/workflows/backend-cd.yaml` | Push to `main`, manual |

- Lint and test run in parallel; build runs only after both pass.
- Docker images are tagged with the Git commit SHA and pushed to Amazon ECR.
- Deployment uses kustomize and kubectl to apply the manifests to EKS.
- The frontend is built with `REACT_APP_MOVIE_API_URL` passed as a build argument.
- AWS credentials are stored in GitHub Secrets only.

## Environment

- Amazon EKS 1.32, region `us-east-1`
- Infrastructure provisioned with Terraform (`setup/terraform`)

## Screenshots

| File | Shows |
|---|---|
| `screenshots/01-frontend-movie-list.png` | Frontend displaying the movie list |
| `screenshots/02-backend-movies-json.png` | Backend `/movies` API response |
| `screenshots/03-all-workflows-green.png` | All four workflows passing |
| `screenshots/04-ecr-backend-image.png` | Backend image in ECR tagged with commit SHA |
| `screenshots/05-ecr-frontend-image.png` | Frontend image in ECR tagged with commit SHA |
| `screenshots/06-failing-test-blocks-build.png` | Failing test prevents the build job |
