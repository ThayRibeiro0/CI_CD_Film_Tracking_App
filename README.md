# CI/CD Pipeline with GitHub Actions and Render Deployment

## Description

This project demonstrates a basic **CI/CD pipeline** setup using **GitHub Actions** to automate testing and deployment for a full-stack application.

- When a **pull request** is made to the `develop` branch, **Cypress component tests** are automatically run.
- When changes are merged into the `main` branch, the application is automatically **deployed to Render** using a deploy hook.

## Technologies Used

- GitHub Actions
- Cypress (for component testing)
- Render (for deployment)
- Node.js / Express / MongoDB (application stack)

## Setup Instructions

1. Download starter code and push it to a new GitHub repo.
2. Set up `develop` and `main` branches.
3. Add GitHub Actions YAML files under `.github/workflows/`.
4. Deploy app manually to Render the first time.
5. Turn off auto-deploy on Render and copy the deploy hook.
6. Add `RENDER_DEPLOY_HOOK_URL` to GitHub repository secrets.

## GitHub Actions

- `.github/workflows/checking_tests.yml` → Runs Cypress tests on PR to `develop`
- `.github/workflows/deploy_to_render.yml` → Deploys app to Render on merge to `main`

## Screenshots

### ✅ Test Workflow
![GitHub Actions Cypress Test](./screenshot/test-success.png)
### 🚀 Deploy Workflow
![GitHub Actions Render Deploy](./screenshot/render-deploy.png)


## Deployed Application

[Film_Tracking_App]()

## Notes

> This project is part of the **Module 20 Challenge** for the UCI Full-Stack Bootcamp.  

## License

This project is licensed under the MIT License.
