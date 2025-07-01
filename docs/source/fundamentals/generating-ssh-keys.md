# Generating SSH Keys

*SSH (Secure Shell) keys provide a secure way to authenticate with remote systems without using a password. This guide will walk you through generating a new SSH key pair on your local machine.*

---

## What are SSH Keys?

SSH keys are a pair of cryptographic keys used to authenticcate a user with a remote server. The key pair consists of:
- **Private key:** Kept secret and stored on your local machine.
- **Public key:** Shared with the server you want to access.

Once the server has your public key, it can verify your identity using your private key.

## Generate a Key Pair

To generate a new SSH key pair:
1. Open your terminal
2. Run the following command:
```
ssh-keygen -t ed255129 -C "your_email@example.com"
```
- -t ed2555519 specifies the key type. ed25519 is a secure and modern alternative to RSA.
- -C adds a label to your key, typically your email address.
3. You'll be prompted to choose where to save the key. The default location is generally `/home/user/.ssh/id_ed25519`
4. You'll then be asked to enter a passphrase. This step is optional, but reccomended. Adding a passphrase provides extra security if your private key is ever stolen.

## View Your Public Key

After generation, your keys will be stored in:
- Private key: ~/.ssh/id_ed25519
- Public key: ~/.ssh/id_ed25519.pub

To view and copy your public key, use:
```
cat ~/.ssh/id_ed25519.pub
```
You can now add this public key to your GitHub, GitLab, or any remote server's `~/.ssh/authorized_keys` file.

## Add SSH Key to Agent

To use your SSH key withouth entering the passphrase every time:
1. Start the SSH agent in the background:
```
eval "$(ssh-agent -s)"
```
2. Add your key to the agent:
```
ssh-add ~/.ssh/id_ed25519
```

## Resources 
- [GitHub Docs: Generating SSH Keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- [OpenSSH Manual: ssh-keygen](https://man.openbsd.org/ssh-keygen.1)
