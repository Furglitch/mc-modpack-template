# Minecraft Modpack Template
A repo template for developing Minecraft modpacks, utilizing packwiz

## Using This Template


### Setting Up Your Repository
To create a new modpack project using this template, click the "Use this template" button at the top of the page. This will create a new repository in your GitHub account with the same directory structure and files as this template.

After creating your repository, you'll want to enable GitHub Actions in your repository settings to use the predefined workflows. The setting can be found under `Settings` > `Actions` > `General`. Set the `Allow all actions and reusable workflows` option and change the `Workflow permissions` to `Read and write permissions`.

After that, use the 'Create New Modpack' workflow in the `Actions` tab to initialize your modpack. It will have you provide your modpack's name, version, and author. This will update pack.toml and other necessary files with your modpack's information.

### Setting Up Your Modpack

2. Clone the repository to your local machine using Git.
    ```bash
    git clone <your-repo-url> -b <branch> '<desired-folder>'
    ```
3. Navigate to the project directory.
    ```bash
    cd '<desired-folder>'
    ```
4. Open the project in your preferred code editor (e.g., VSCode).
5. Set up packwiz by following the instructions in the [Using Packwiz](#using-packwiz) section below.

### Using Packwiz
This template is set up to use [packwiz](https://packwiz.infra.link/) for managing mods and other resources. To get started with packwiz:
1. Install packwiz on your machine by following the instructions [here](https://packwiz.infra.link/installation/).
2. Open a terminal in your project directory and navigate to the `/packwiz/` folder.</br>
    ```bash 
    cd packwiz
    ```

3. Use packwiz commands as described in the [packwiz documentation](https://packwiz.infra.link/tutorials/creating/adding-mods/) to add, remove, and manage mods for your modpack.
    ```bash
    packwiz curseforge add <mod-id>
    ```

4. If you make a change inside the `/packwiz/` folder without the `packwiz` command, make sure to run:
    ```bash
    packwiz refresh
    ```

### The 'Server' Folder
This template includes a `server` folder that contains files necessary for running a dedicated Minecraft server for your modpack. This includes startup scripts and Java args.

This is also where you'd put any server-specific configuration files such as `server.properties` or `server-icon.png`.

NOTE: The startup scripts have the placeholder 'NEOFORGE_VERSION' in them, which will be automatically replaced with the correct version number when being built by the GitHub Actions workflow.


## Action Workflows
This modpack template includes predefined GitHub Actions workflows to automate common tasks such as building and updating your modpack.

### modpack-build.yml
This workflow automatically builds your modpack whenever changes are pushed to the branch. It also runs on pull requests targeting the branch. 

It generates three files, two client-side files (.zip for CurseForge and .mrpack for Modrinth) and one server-side .zip file. These files are stored as artifacts in the workflow run, which you can download and use to distribute your modpack.

### modpack-update.yml
This workflow checks for updates to the mods and other resources in your modpack every two days. If updates are found, it automatically creates a pull request with the updated files.

### packwiz-refresh.yml
This workflow runs `packwiz refresh` on the `/packwiz/` folder whenever a push is made to the branch. This ensures that the packwiz metadata is always up to date. This also runs on pull requests targeting the branch to ensure consistency before merging.

### issue-title.yml
The issue templates in this repository have placeholders such as `{modpack_version}` and `{mod_name}`. This workflow will automatically replace these placeholders based on what the user has filled out in the form when they create a new issue.

## Issue Templates
This modpack template includes predefined issue templates to help your users report bugs and make requests. You can customize these templates by editing the files in the [`.github/ISSUE_TEMPLATE/`](./.github/ISSUE_TEMPLATE/) directory.

## Tips and Tricks

### Multi-Platform Mods
For mods that are available on both CurseForge and Modrinth, you should use the source where you plan to distribute your modpack.

If you plan to distribute your modpack on Modrinth, they only allow mods from their own platform.

CurseForge, on the other hand, has [a list](https://docs.google.com/spreadsheets/d/176Wv-PZUo9hFxy6oC6N8tWdquBLPRtSuLbNK-r0_byM) of allowed mods from third-party sources. If the mod you want to use is on that list, you can add it to your modpack from the listed source.

### Recommended Mods
Recommended mods for modpack development:

  - **Modpack Update Checker**: Notifies players of modpack updates in-game. Just update a file in the root of the git repo!</br>Get it on [*CurseForge*](https://www.curseforge.com/minecraft/mc-mods/modpack-update-checker) and [*Modrinth*](https://modrinth.com/mod/modpack-update-checker).

  - **Paxi**: Hard-loads resource packs and data packs to ensure they are always applied.</br>Get it on [*CurseForge*](https://www.curseforge.com/minecraft/mc-mods/paxi-neoforge) and [*Modrinth*](https://modrinth.com/mod/paxi).

  - **Packed Packs**: An alternative (or complement) to *Paxi*. Allows you to create 'profiles' of predetermined, sorted pack lists for players to choose from.</br>Get it on [*CurseForge*](https://www.curseforge.com/minecraft/mc-mods/packed-packs) and [*Modrinth*](https://modrinth.com/mod/packed-packs).

  - **Configured Defaults**: Allows you to set config defaults that won't be overridden by pack updates, for things such as keybinds and resource pack selections (options.txt).</br>Get it on [*CurseForge*](https://www.curseforge.com/minecraft/mc-mods/configured-defaults) and [*Modrinth*](https://modrinth.com/mod/configured-defaults).

  - **KubeJS**: Allows for custom scripts to add custom content and tweak existing content, without needing to create a full mod.</br>Get it on [*CurseForge*](https://www.curseforge.com/minecraft/mc-mods/kubejs) and [*Modrinth*](https://modrinth.com/mod/kubejs).

  - **Memory Settings**: Lets you set a recommended RAM range. If the player is outside of that range, it will warn them.</br>Get it on [*CurseForge*](https://www.curseforge.com/minecraft/mc-mods/memory-settings).

  - **Crash Assistant**: Shows a GUI after a crash, allowing players to easily gather logs for issue reports.</br>Get it on [*CurseForge*](https://www.curseforge.com/minecraft/mc-mods/crash-assistant) and [*Modrinth*](https://modrinth.com/mod/crash-assistant).