# PenguinOS

PenguinOS is an Android distribution based on [Paranoid Android](https://github.com/AOSPA).
This manifest contains Project PenguinOS CLO for OnePlus 13R/Ace5.

## Device Specific Features

For device specific features, the following commits must be merged:
- https://github.com/AOSPA/android_packages_apps_Settings/commit/1ac1a658f66f10ba77bbde22b4c2fb6ce0c79b3b
- https://github.com/AOSPA/android_packages_apps_Settings/commit/cec0d825c4f88918a19553031f22a0d9c121d255
- https://github.com/DerpFest-AOSP/android_frameworks_base/commit/18e6d309997b19f59655ac140d210a02fd351fa0
- https://github.com/aosp-for-giulia/derp_android_packages_apps_Settings/commit/e2947326eab02ce1cf0aeded57822992fd891c32

## Set up your machine

You must run a 64-bit Linux distribution to build PenguinOS.
Follow the system setup instructions on the [Android Open Source Project website](https://source.android.com/source/initializing.html#setting-up-a-linux-build-environment).
Google provides Ubuntu-specific setup packages and instructions.
Complete the environment setup before you proceed.

## Obtain the source

[Repo](https://source.android.com/source/developing.html) is a tool provided by Google that simplifies using [Git](https://git-scm.com/book) with Android source trees.

### Install Repo

Create a directory for `repo` and add it to your `PATH`:
```bash
mkdir -p ~/.local/bin
export PATH=~/.local/bin:$PATH
```

Download the `repo` binary:
```bash
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/.local/bin/repo
```

Make the binary executable:
```bash
chmod a+x ~/.local/bin/repo
```

### Initialize Repo

Create a working directory on a case-sensitive filesystem and navigate into it.
Replace `WORKSPACE` with your chosen directory path.
```bash
mkdir WORKSPACE
cd WORKSPACE
```

Initialize the manifest repository:

> [!IMPORTANT]
> Configure your real name and email address in Git before you initialize Repo if you plan to submit patches.

```bash
repo init -u https://github.com/ronardnx/manifest -b celerity
```

### Download the source tree

Run `repo sync` to pull upstream source code.

> [!NOTE]
> Initial synchronization downloads the entire source history and takes significant time.

The `-j` option specifies the number of concurrent network jobs.
```bash
repo sync --current-branch --no-tags -j4
```

> [!TIP]
> A value of four jobs (`-j4`) works well for most internet connections.
> Adjust this value based on your connection speed.

#### Sync specific projects

You can synchronize individual projects instead of the entire source tree.
Specify projects by repository path or remote name.

> [!WARNING]
> Partial synchronization can cause build failures if changes span across projects.

For example, specify `frameworks/base` or `Project-PenguinOS/frameworks_base`:
```bash
repo sync PROJECT
```

## Build

The bundled builder script `./rom-build.sh` automates all build steps for a target device.
Provide the target device codename as the argument (for example, `sky` for POCO M6 Pro 5G, or `marble` for POCO F5).

Navigate to your workspace root and execute the build script:
```bash
cd WORKSPACE
./rom-build.sh DEVICE
```

## Submit patches

PenguinOS is open source and accepts patches from contributors.
Changes are reviewed as pull requests on [GitHub](https://github.com/Project-PenguinOS).

### Create a branch

Navigate to your workspace root:
```bash
cd WORKSPACE
```

Create a topic branch for the project you want to modify.
Identify the project by repository name or local directory path:

| Identify by | Command |
| --- | --- |
| Repository name | `repo start BRANCH Project-PenguinOS/PROJECT` |
| Directory path | `repo start BRANCH PROJECT_DIR` |

For example, start a branch for `frameworks/base` (`Project-PenguinOS/frameworks_base`):
```bash
repo start BRANCH frameworks/base
```

### Commit and push

Navigate to the project directory:
```bash
cd PROJECT_DIR
```

Make your code changes, then stage and commit them:
```bash
git add -A
git commit -a -s
```

Push the branch to your fork and open a pull request against `celerity`.
Replace `USERNAME` with your GitHub username and `PROJECT` with the repository name.
```bash
git push git@github.com:USERNAME/PROJECT HEAD:BRANCH
```

### Make additional changes

To update an open pull request, amend the previous commit and force-push the branch:
```bash
git commit -a --amend
git push --force-with-lease git@github.com:USERNAME/PROJECT HEAD:BRANCH
```

### Squash multiple commits

Each submitted patch must be a single commit.
Squash multiple commits before you push:
```bash
git rebase -i HEAD~<commit-count>
```

### Write commit messages

Write clear and descriptive commit messages.

- Use the imperative mood in the subject line (for example, "Fix audio routing", not "Fixed audio routing").
- Keep the subject line near 50 characters and under 72 characters.
- Capitalize the first word of the subject line and omit trailing periods.
- Prefix the subject with the relevant project or component name when appropriate (for example, `manifest: Update default branch`).
- Keep the subject line as the whole message unless the reason for the change is not evident from the diff.
- Separate the subject line from the message body with a blank line.
- Wrap message body text at 72 characters.

## Project assets and licensing

### Source code

The codebase uses the Apache License, Version 2.0 unless otherwise specified.
Retain all copyright and license notices when you use or modify the source code.
State any modifications you make to the code.
Read the full license text at https://www.apache.org/licenses/LICENSE-2.0.

### Images and branding assets

Unless otherwise specified, all project assets (including images and branding) use the Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0) license.
You may share and adapt these assets for non-commercial purposes.
You must provide attribution to the original author (PenguinOS).
Include a reference to the license and note any modifications.
Read the full license text at https://creativecommons.org/licenses/by-nc/4.0/.
