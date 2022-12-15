# Development workflow

Forest Admin lets you get started easily, but soon you'll be wondering how to set up a clean workflow to control every step of your development process.

The following workflow requires that you have generated your project and pushed it to Production. If it's not the case, check out our quick start.

Here's our **recommended development workflow**:

#### Step 1: Install forest-cli <a href="#step-1-install-forest-cli" id="step-1-install-forest-cli"></a>

We've developed a **CLI tool** to help you seamlessly control your layout (UI) as you develop. You should first install it:

npm install -g forest-cli

For further details on the package, check out [this page](https://www.npmjs.com/package/forest-cli).

#### Step 2: Set up your development environment <a href="#step-2-set-up-your-development-environment" id="step-2-set-up-your-development-environment"></a>

This step is **not necessary** if you are the creator of the project, as your development environment is already generated.

To get started with forest-cli, simply run the following command in your project's folder:

This will create a development environment for you to develop locally in.

For a more in-depth walkthrough of the `init` command, check out this page.

Got a new feature to develop? Create a branch based on the origin environment you want!

forest branch my-new-feature --origin the-origin-environment

Your new branch is now available with a layout you can play with.

For a more in-depth walkthrough of the `branch` command, check out this page.

#### Step 4: Develop your feature <a href="#step-4-develop-your-feature" id="step-4-develop-your-feature"></a>

Your feature may require frontend (layout) and backend changes.

Your feature works as intended on your local branch? You now need to deploy it to your production environment:

* Deploy backend changes (if any) using your usual workflow
* Deploy frontend changes using the following command:

That's it! Your new feature is now available in production 🎉
