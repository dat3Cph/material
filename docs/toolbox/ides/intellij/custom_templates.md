---
title: Custom templates
description: How to make your own custom templates in IntelliJ IDEA
layout: default
nav_order: 1
parent: IDEs
grand_parent: Toolbox
permalink: /toolbox/ides/intellij/custom-templates
---

# Custom templates

Creating a custom project template in IntelliJ IDEA allows you to save your current project setup, including files, configurations, and dependencies, so you can reuse it for future projects. We sometimes call these templates for "boilerplates", "starter projects" or "startcode".

## Setting up a custom template

Here’s how you can create a custom template:

### 1. **Set Up Your Project**

- Open IntelliJ IDEA.
- Create a new project or open an existing one that you want to use as the base for your custom template.
- Configure the project as needed, including:
  - Adding dependencies (e.g., Maven, Gradle, libraries).
  - Setting up the project structure.
  - Creating any necessary files or folders.
  - Configuring settings such as code style, run configurations, etc.

### 2. **Save the Project as a Template**

- Once your project is fully set up, go to the main menu and select `File` > `New Projects Setup` > `Save as Template...`.
- In the dialog that appears, you can do the following:
  - **Template Name**: Enter a name for your template.
  - **Description**: Optionally, provide a description for the template to remind you what it includes or is intended for.
  - **Include Files and Directories**: By default, IntelliJ IDEA will include all the files and directories in your project. If you want to exclude any files, you can specify them here.
- Click `OK` to save the template.

## How to use your custom template

### 1. **Using Your Custom Template**

- The next time you create a new project, you can use your custom template:
  - Go to `File` > `New` > `Project...`.
  - In the "New Project" wizard, look for the option to select a project template. Your custom template should appear in the list under the relevant language or framework section.
  - Select your custom template and proceed to create your new project. The new project will be set up with all the configurations, files, and dependencies from the template.

### 2. **Managing and Editing Custom Templates**

- If you want to manage your templates (e.g., rename or delete them), you can manually navigate to the location on disk where they are stored:
  - **Windows**: `C:\Users\<YourUsername>\.IntelliJIdea<version>\config\projectTemplates`
  - **macOS**: `/Users/<YourUsername>/Library/Application Support/JetBrains/IntelliJIdea<version>/projectTemplates`
  - **Linux**: `/home/<YourUsername>/.config/JetBrains/IntelliJIdea<version>/projectTemplates`
- You can manually edit or delete the template files stored in these directories if needed.

### 3. **Tips for Creating Effective Templates**

- **Keep It Generic**: Create templates that can be reused in different projects. Avoid hardcoding project-specific details.
- **Include Only Necessary Files**: Exclude unnecessary files, such as `README.md` or `.gitignore`, if they won’t be useful in all projects.
- **Test the Template**: After creating the template, test it by creating a new project from it to ensure everything works as expected.

Creating custom templates can save you a lot of time by providing a consistent starting point for your projects, especially when working with specific setups or repetitive project configurations.

## Example Template for JPA

If you're working with Java Persistence API (JPA) projects, you might want to create a custom template that includes the necessary dependencies, configurations, and project structure for JPA projects. Here's an example of "installing" and using such a template:

1. **Download the Template**: [Template for IntelliJ IDEA JPA/DeepDive weeks](./download/dd_startcode.zip)
2. Move the template (zip-file) to IntelliJ's `projectTemplates" folder on your local machine.
    - **Windows**: `C:\Users\<YourUsername>\.IntelliJIdea<version>\config\projectTemplates`
    - **macOS**: `/Users/<YourUsername>/Library/Application Support/JetBrains/IntelliJIdea<version>/projectTemplates`
    - **Linux**: `/home/<YourUsername>/.config/JetBrains/IntelliJIdea<version>/projectTemplates`
    - You can manually edit or delete the template files stored in these directories if needed.
3. **Create a New Project from the Template**:
    - Open IntelliJ IDEA.
    - Go to `File` > `New` > `Project...`.
    - Look for the option to select a project template (buttom of the window).
    - Select the `dd_startcode` template and proceed to create your new project.
