## Notes on Hosting Static sites and working with node or other (flutter/html etc) frontends
 We will use flutter as an example. 

### PREPARE the REPO (ONE TIME TASKS)
To set up a Flutter build for
GitHub Pages, follow these steps to build your web app and host it as a static site. 
1. Prepare Your Flutter Project
Ensure your project is configured for web support before building. 

    Enable Web Support: Run flutter config --enable-web if it isn't already enabled.
    Inject Web Support: If your project lacks a web/ folder, run flutter create --platforms=web . in your project root. 

### DO EACH BUILD
2. Build the Static Files
Run the build command to generate the production-ready HTML, CSS, and JavaScript files. 

    Base Href: If hosting at username.github.io/repository_name/, you must set the base href to match your repository name to avoid a blank screen.
    Command: flutter build web --release --base-href /repository_name/.
    Output: The static files will be generated in the build/web directory. 

### DEPLOY (SETUP OR AUTOMATE buildserver or github pages etc)
3. Deploy to GitHub Pages 
You can deploy manually or automate the process using GitHub Actions. 
Option A: Manual Deployment

    Initialize Git in Build Folder: Navigate to build/web, run git init, and add all files.
    Push to GitHub: Add your remote repository and push these files to a specific branch (e.g., gh-pages or main).
    Configure Settings: In your GitHub repository, go to Settings > Pages. Under Build and deployment, select your deployment branch and set the folder to / (root). 

Option B: Automated Deployment (Recommended)
Use a GitHub Action to automatically rebuild and deploy whenever you push to your main branch. 

    Workflow File: Create a file at .github/workflows/deploy.yml.
    Action used: Use community-tested actions like bluefireteam/flutter-gh-pages or peaceiris/actions-gh-pages to handle the deployment to the gh-pages branch.
    Permission: Ensure your workflow has contents: write permissions to allow it to push the build artifacts to your repository. 

### HOSTING on your own domain/server notes 
4. Custom Domains (Optional)

    GitHub Settings: Add your custom domain in the Pages section of your repository settings.
    DNS Configuration: Add a CNAME record in your domain registrar's settings (e.g., Namecheap or GoDaddy) pointing to username.github.io.
