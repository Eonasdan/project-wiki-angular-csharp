Git is slightly different compare to VSSC. While many operations are the same or similar they are different enough that it may take some time to learn the differences.

This guide will assume that you have the [Visual Studio git plugin](https://visualstudio.github.com/) and [Git for Windows](https://git-scm.com/downloads).

# Getting Started
## Cloning
The first thing that you need to do in any git project is clone the repository locally.
Go to the Code section of VSTS for the project in question.
![image.png](/.attachments/image-f6345e59-db2d-427d-881b-20b5be898774.png)
1. Click “Clone”
1. Click “Clone in Visual Studio”
![image.png](/.attachments/image-4992428e-7060-45c2-ad77-a54c0190b1f4.png)
1. After Visual Studio opens, you will be prompted to select a local path to clone the repository to. This destination is entirely up to you.
1. Click “Clone”
1. Once the cloning process is complete, follow the steps in “Living with Angular”

## Living with Angular
You will need to run `npm install` from the `ClientApp` directory before your first run to install client side dependencies.

Angular projects will also include a script that will continuously monitor any changes to typescript files and automatically rebuild as needed. This can be done as `npm run watch` or `ng build --watch` from the ClientApp directory.
