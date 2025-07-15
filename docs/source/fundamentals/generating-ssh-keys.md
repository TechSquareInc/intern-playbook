# 🔐 Generating SSH Keys

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
ssh-keygen -t ed25519 -C "your_email@example.com"
```
- `-t ed25519` specifies the key type.
- `-C` adds a label to your key, typically your email address.
3. You'll be prompted to choose where to save the key. The default location is generally `/home/user/.ssh/id_ed25519`
4. You'll then be asked to enter a passphrase. This step is optional, but reccomended. Adding a passphrase provides extra security if your private key is ever stolen.

## View Your Public Key

After generation, your keys will be stored in:
- Private key: `~/.ssh/id_ed25519`
- Public key: `~/.ssh/id_ed25519.pub`

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

## Ed25519 vs RSA
- **RSA** stands for **Rivest-Shamir-Adleman** and is a type of public-key cryptography algorithm that is used with legacy system compatibility. RSA uses an asymmetric algorithm that's based on integer factorization. It is generally slower and requires longer keys to meet modern standards. The key file format is similar to Ed25519 and reads like `id_rsa/id_rsa.pub`.
- **Ed255519** is a high-security, high-performance digital signature scheme. It is asymmetric and is based on elliptic curve cryptography, specifically the **Edwards-curve Digital Signature Algorithm (EdDSA)** and utilizes the **Curve25519** elliptic curve. It is generally faster, is fixed at a size of 256 bits, and is designed for modern cryptographic needs. The key file format reads like `id_ed25519/id_ed25519.pub`.

## Resources 
- [GitHub Docs: Connecting to GitHub with SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh): Resources about SSH and connecting to GitHub.
- [GitHub Docs: Generating New SSH Keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent): Generate SSH keys to enable authentication for Git operations over SSH.
- [OpenSSH Manual: ssh-keygen](https://man.openbsd.org/ssh-keygen.1): Deep dive on `ssh-keygen`, the OpenSSH authentication key utilty.
- [OpenSSH Key Generating](https://help.ubuntu.com/community/SSH/OpenSSH/Keys): Description of public and private keys, how to generate them for key-based SSH logins.
- [RSA vs Ed25519](https://www.geeksforgeeks.org/devops/rsa-vs-ed25519-which-key-pair-is-right-for-your-security-needs/): An overview of the key differences of these two prominent types of key pairs.
