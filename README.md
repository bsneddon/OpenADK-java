OpenADK (Java version)
======================

The ADK is licensed under the Apache 2.0 Software License. Copyright in the ADK is held by Pearson and by the community contributors to the ADK project. The license is in the file LICENSE-2.0.txt in the ADK folder after installation. Note that the Apache license does not require you to make any of your application's code available as open source software.

All files under the Apache license may be redistributed in binary and/or source form with your agent, although only a subset is actually needed by most agents (the contents of the lib directory are usually required). Note that some files may be under the same or a different open source license and subject to third-party license agreements included in the licenses directory.

Overview
--------
There are a couple of ways for building the OpenADK. Please refer to the 'Readme' files in each sub-directory for detailed build instructions.

If you are using Eclipse it is suggested to import the top level project (OpenADK-java) into Eclispe and then import all other sub-projects (adk-generator, adk-library & adk-examples) into Eclipse. After this initial import the projects may show up with errors. It is required to build the adk-generator and adk-library first and then 'refresh' the projects to remove these errors. Please refer to build instructions in appropriate Readme file. 


Contributing
------------

For some background information regarding the branching model used by this project, refer to the article [A successful Git branching model][1]. The ideas from that article have been combined with the collaborative development techniques recommended by GitHub (specifically [Using Pull Requests][2]) to form these procedures.

### Pre-requisities ###

* [Git][3] installed.
* A strong understanding of Git. For an introduction, read [Getting Started - Git Basics][4].
* A GitHub account and Pull access to the [OpenADK][5] repositories.

### Defined Repositories ###

The procedures following refer to 3 Git repositories:

* The remote [OpenADK-java][8] repository containing a _central_ copy of the code.
* Your remote repository created within your GitHub account.
* Your local repository residing on your local machine.

### Getting the code ###

1. Fork the [OpenADK-java][8] repository into your remote repository (click on the "Fork" button).
2. Clone your fork to create your local repository. This will create a _OpenADK-java_ directory on your local machine.

    ```dos
    c:\dev> git clone https://github.com/USERNAME/OpenADK-java.git
    ```

3. Add the _upstream_ ([OpenADK-java][8]) repository as a remote. This will allow you to keep track of the [OpenADK-java][8] repository and pull in updates.

    ```dos
    c:\dev> cd OpenADK-java
    c:\dev\OpenADK-java> git remote add upstream git://github.com/open-adk/OpenADK-java.git
    ```

4. Create a _topic_ branch in your remote repository based upon the _develop_ branch and switch to it (your local repository). __Do not base your _topic_ branch on any other branch!__

    ```dos
    c:\dev\OpenADK-java> git checkout -t origin/develop
    c:\dev\OpenADK-java> git branch ISSUE_XXX develop
    c:\dev\OpenADK-java> git checkout ISSUE_XXX
    ```

### Submitting a change ###

5. Ensure that all changes applied to the _topic_ branch (locally) have been committed to your remote repository (with an appropriate message). The _-a_ flag skips _staging_.

    ```dos
    c:\dev\OpenADK-java> git commit -a -m MESSAGE
    ```

6. Before submission, ensure that your remote repository is up-to-date.

    ```dos
    c:\dev\OpenADK-java> git checkout develop
    c:\dev\OpenADK-java> git fetch upstream
    c:\dev\OpenADK-java> git merge upstream/develop
    ```

7. Rebase the changes in your local repository (making for a cleaner history).

    ```dos
    c:\dev\OpenADK-java> git checkout ISSUE_XXX
    c:\dev\OpenADK-java> git rebase develop
    ```

8. Resolve and recommit [merge conflicts][7] (if any), and continue the rebase.

    ```dos
    c:\dev\OpenADK-java> git rebase --continue
    ```

9. Push your local changes to your remote repository.

    ```dos
    c:\dev\OpenADK-java> git push origin ISSUE_XXX
    ```

### Issue a Pull Request ###

The [Using Pull Requests][2] article provides a comprehensive guide for issuing a Pull Request.

10. Browse to your remote (forked) repository on the GitHub site.

11. Swith to the *ISSUE_XXX* branch and press the "Pull Request" button.

12. Review the Pull Request details and provide a meaningful title (with issue number if appropriate) and description of your change. It is important to ensure that the _base branch_ is set to _develop_ and the _head branch_ is set to *ISSUE_XXX*.

13. Press the "Send pull request" button.

### Completion of a Pull Request ###

Pull Requests are automatically closed when the requested commits are merged into the [OpenADK-java][8] repository. However, a number of other tasks may be helpful once your changes have been accepted and processed.

14. Remove the *ISSUE_XXX* branch both from your local repository and your remote repository.

    ```dos
    c:\dev\OpenADK-java> git branch -d *ISSUE_XXX*
    c:\dev\OpenADK-java> git push origin --delete *ISSUE_XXX*
    ```

15. Update the _develop_ branch of your remote repository with the latest version of the [OpenADK-java][8] repository.

    ```dos
    c:\dev\OpenADK-java> git checkout develop
    c:\dev\OpenADK-java> git fetch upstream
    c:\dev\OpenADK-java> git merge upstream/develop
    c:\dev\OpenADK-java> git push origin develop
    ```

Project Maintenance
-------------------

### Merge a Pull Request ###

GitHub provides the ability for a Pull Request to be automatically merged. If you have the appropriate permissions, the "Merge pull request" button can be used from the "Pull Requests" page. Alternatively, you could perform a manual merge on the command line.

1. Check out a new branch of the [OpenADK-java][8] repository to test the changes in.

    ```dos
    c:\dev\OpenADK-java> git checkout -b USERNAME-ISSUE_XXX develop
    ```

2. Bring in the changes from the requesting repository into your new branch and perform your tests.

    ```dos
    c:\dev\OpenADK-java> git pull https://github.com/USERNAME/OpenADK-java.git ISSUE_XXX
    ```

3. Merge the changes and update the [OpenADK-java][8] repository.

    ```dos
    c:\dev\OpenADK-java> git checkout develop
    c:\dev\OpenADK-java> git merge USERNAME-ISSUE_XXX
    c:\dev\OpenADK-java> git push origin develop
    ```

### Creating a released version in master ###

1. Merge from _release_ to _master_.

2. Tag (annotated) the _master_ branch with an appropriate release number and share it with the [OpenADK-java][8] repository.

    ```dos
    c:\dev\OpenADK-java> git checkout master
    c:\dev\OpenADK-java> git tag -a X.X.X -m MESSAGE
    c:\dev\OpenADK-java> git push origin X.X.X
    ```

### Creating a hotfix ###

The following steps need to be performed within your remote repository. __Care should be taken as these steps operate directory on the _master_ branch.__

1. Create a new _topic_ branch within your remote repository for the hotfix.

    ```dos
    c:\dev\OpenADK-java> git checkout -b HOTFIX_XXX master
    ```

2. Apply your changes to the *HOTFIX_XXX* branch.

3. Commit your changes.

    ```dos
    c:\dev\OpenADK-java> git commit -a -m MESSAGE
    ```

4. Push your local changes to your remote repository.

    ```dos
    c:\dev\OpenADK-java> git push origin HOTFIX_XXX
    ```

5. Browse to your remote (forked) repository on the GitHub site.

6. Switch to the *HOTFIX_XXX* branch and press the "Pull Request" button.

7. Review the Pull Request details and provide a meaningful title (with issue number if appropriate) and description of your change. It is important to ensure that the _base branch_ is set to _master_ and the _head branch_ is set to *HOTFIX_XXX*.

8. Press the "Send pull request" button.

The following steps need to be performed within the [OpenADK-java][8] repository.

9. Browse to the [OpenADK-java][8] repository on the GitHub site.

10. Find the Pull Request and merge it (using the "Merge pull request" button).

11. __Before updating the (tag) version number, ensure that locally the code is up-to-date.__ Tag (annotated) the _master_ branch with an appropriate release number and share it with the [OpenADK-java][8] repository. With a hotfix submission, increment the third digit of the version number by 1.

    ```dos
    c:\dev\OpenADK-java> git checkout master
    c:\dev\OpenADK-java> git tag -a X.X.X -m MESSAGE
    c:\dev\OpenADK-java> git push origin X.X.X
    ```

12. Merge the changes into the develop branch.

    ```dos
    c:\dev\OpenADK-java> git checkout develop
    c:\dev\OpenADK-java> git fetch origin
    c:\dev\OpenADK-java> git merge origin/master
    c:\dev\OpenADK-java> git push origin develop
    ```

[1]: http://nvie.com/posts/a-successful-git-branching-model
[2]: https://help.github.com/articles/using-pull-requests
[3]: http://git-scm.com/downloads
[4]: http://git-scm.com/book/en/Getting-Started-Git-Basics
[5]: https://github.com/organizations/open-adk
[6]: forkButton.png "Fork"
[7]: http://git-scm.com/book/en/Git-Branching-Basic-Branching-and-Merging#Basic-Merge-Conflicts
[8]: https://github.com/open-adk/OpenADK-java
[9]: http://symfony.com/doc/current/contributing/code/patches.html
