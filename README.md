# maven-bintray-github-actions
An example of how to publish an artifact to bintray using github actions.

1. Package will be created if it does not exist using https://github.com/benjefferies/create-bintray-package
  ```
    - name: Create Package
    uses: benjefferies/create-bintray-package@master
    with:
      bintray-user: benjefferies
      bintray-token: ${{ secrets.BINTRAY_ACCESS_TOKEN }}
      owner: benjefferies
      repo: openbanking4.dev
      package-name: maven-bintray-github-actions
      package-description: Example
      package-url: https://github.com/benjefferies/maven-bintray-github-actions
      package-license: MIT
  ```
1. Then we will publish the artifact using https://github.com/qcastel/github-actions-maven-release
  ```
    - name: Release
    uses: qcastel/github-actions-maven-release@master
    with:
      release-branch-name: "master"
      gpg-enabled: "true"
      gpg-key-id: ${{ secrets.GITHUB_GPG_KEY_ID }}
      gpg-key: ${{ secrets.GITHUB_GPG_KEY }}
      maven-repo-server-id: bintray-benjefferies-openbanking4.dev
      maven-repo-server-username: ${{ secrets.PRIVATE_REPO_USER }}
      maven-repo-server-password: ${{ secrets.PRIVATE_REPO_PASSWORD }}
      maven-args: "-Dmaven.javadoc.skip=true -DskipTests -DskipITs -Ddockerfile.skip -DdockerCompose.skip"
      git-release-bot-name: "bot"
      git-release-bot-email: "bot@echosoft.uk"
      access-token: ${{ secrets.ACCESS_TOKEN }}
  ```
