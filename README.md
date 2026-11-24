# BlueBuild Template &nbsp; [![bluebuild build badge](https://github.com/blue-build/template/actions/workflows/build.yml/badge.svg)](https://github.com/blue-build/template/actions/workflows/build.yml)

1. Open https://github.com/butrelinux/bluebuild-template.
2. Press “Use this template” and create a new repository.  
3. Set up container signing
    1. Clone your repository
    2. Within your repository, generate a new key pair with ```cosign generate-key-pair```
    3. When prompted for a password, just press enter.  This will be used in GitHub Actions and cannot be encrypted.
    4. Set the signing secret with ```gh secret set SIGNING_SECRET < cosign.key```
4. Change the name: in recipes/recipe.yml and commit your changes. You can also apply some initial customizations here.  
5. Open the Actions tab of your repository and make sure GitHub Actions are enabled.  
6. Change all references to butrelinux/bluebuild-template in the README.md to the details of your repository or custom image and commit your changes. You should also change the title and the short description below it so that people stumbling on your repository know what they are looking at.  
7. You’re done! You can now open recipes/recipe.yml and start customizing! The reference section of the documentation is your friend here.  


## Installation

> [!WARNING]  
> [This is an experimental feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable), try at your own discretion.

To rebase an existing butrelinux image to your own build
```bash
# this is just an example.  change the username in this image to your own.
# if you change the package name or the tag, you'll need to change that too
sudo bootc switch --enforce-container-sigpolicy ghcr.io/octocat/butrelinux-personal:latest
```

The `latest` tag will automatically point to the latest build. That build will still always use the Fedora version specified in `recipe.yml`, so you won't get accidentally updated to the next major version.

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/blue-build/template
```
