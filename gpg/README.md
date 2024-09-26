[![Github logo](https://www.flaticon.com/free-icon/github-logo_25231)](https://github.com)

# Setup GPG Key on Github

Here is a small tutorial to setup a GPG key on your `GitHub account`.

The GPG key will allow us to be more secure when committing, mostly by authenticating and signing when committing.

#### Setup

1. **Generate the GPG key** (Enter name and email address). The output should return the id of your public GPG key.

```bash
gpg --full-generate-key
```

2. **Setting up your GPG signing key on your git account.**

```bash
git config --global user.signingkey <public GPG Key ID>
```

3. **Show the content of your public GPG key.**

```bash
gpg --armor --export <public GPG Key ID>
```

4. **Add the GPG key on GitHub:** Add the content of your public key to GitHub, in the same place you add an SSH key.

#### Committing

When the setup is done, you can now sign all your commits with the -S flag.

```bash
git commit -S -m "my commit"
```

Your commits are now marked as verified on GitHub.