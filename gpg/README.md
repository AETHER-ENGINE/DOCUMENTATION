# Setup GPG Key on GitHub / GitLab

Here is a small tutorial to setup a GPG key on your `GitHub and/or GitLab account`.

The GPG key will allow us to be more secure when committing, mostly by authenticating and signing when committing.

#### Setup

1. **Generate the GPG key** (Enter name and email address). The output should return the id of your public GPG key.

```bash
gpg --full-generate-key
```

2. **Get the ID of your new GPG key**

```bash
gpg --list-secret-keys --keyid-format=long
```

You will see something like :

```
/home/utilisateur/.gnupg/secring.gpg
-----------------------------------
sec   rsa4096/ABC123456789DEF0 2023-01-01 [SC]
      D4C3A42BC8E01234B56789DEF0ABCDE123456789
uid           [ultimate] Nom d'Utilisateur <email@example.com>
ssb   rsa4096/1234567890ABCDEF 2023-01-01 [E]
```

**Your GPG key ID is the part after "rsa4096/" in the section sec.**
**In this example, your key ID is ABC123456789DEF0.**

3. **Setting up your GPG signing key on your git account.**

```bash
git config --global user.signingkey <public GPG Key ID>
```

# Configuring GPG Keys for GitHub and GitLab

### **On GitHub**
1. **Log in to your GitHub account.**
2. Go to your **user settings**:
   - Click on your avatar in the top-right corner.
   - Select **Settings**.
3. **Add a GPG key:**
   - In the **Access** section of the sidebar, click on **SSH and GPG keys**.
   - Click the **New GPG key** button.
4. **Copy and paste your public key:**
   - In your terminal, run the following command to display your public key:
     ```bash
     gpg --armor --export <public GPG Key ID>
     ```
   - Copy the entire public key, including the markers:
     ```
     -----BEGIN PGP PUBLIC KEY BLOCK-----
     ...key content...
     -----END PGP PUBLIC KEY BLOCK-----
     ```
   - Paste this key into the designated field on GitHub.
5. **Save the key:**
   - Click **Add GPG key**.
   - If prompted, enter your password to confirm.

---

### **On GitLab**
1. **Log in to your GitLab instance (self-hosted or GitLab.com).**
2. Go to your **user settings**:
   - Click on your avatar in the top-left corner.
   - Select **Edit profile**.
3. **Add a GPG key:**
   - In the left-hand sidebar, click on **GPG Keys** (under **User Settings**).
4. **Copy and paste your public key:**
   - Run the following command in your terminal to get your public key:
     ```bash
     gpg --armor --export <public GPG Key ID>
     ```
   - Copy the entire public key, including the markers:
     ```
     -----BEGIN PGP PUBLIC KEY BLOCK-----
     ...key content...
     -----END PGP PUBLIC KEY BLOCK-----
     ```
   - Paste this key into the designated field on GitLab.
5. **Save the key:**
   - Click **Add GPG Key** to finalize.

---

### **Verification**
- **For GitHub**: Verify that your commits display a "Verified" badge in the commit history.
- **For GitLab**: Signed commits will display a lock icon and be marked as "Verified" in the interface.

### **Tip for Automatic Signing**


#### Committing

When the setup is done, you can now sign all your commits with the -S flag.

```bash
git commit -S -m "my commit"
```

You can also define that you wanna sign all your commits by default with the following command:

```bash
git config --global commit.gpgSign true
```

Your commits should now be marked as verified on GitHub.