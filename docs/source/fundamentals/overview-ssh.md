# Overview of SSH

*Remote administration protocol that allows users to control and modify remote hosts.*

----

## The Basics

SSH (Secure Shell) is a protocol used to securely connect to a remote computer over an unsecured network. It provides a channel between a client (your machine) and a server (a remote system).

SSH provides a mechanism for:
- Authenticating a remote user.
- Transfering inputs from a client to a host.
- Relaying output back to a client.

By default, SSH works over TCP port 22 to communicate. It encrypts all data excahgned between the client and server. including all credentials, commands, and output.

## Usage

Basic syntax for connecting would look like: `ssh {USER@REMOTE_HOST}`. 
For example, `ssh tim@example.com` or `ssh chloe@192.168.122.208`. 
Additionally, you could specify what port you would like to connect through, `ssh -p 2222 user@host`, or run a single command on a remote system, `ssh user@host 'ls -la'`.

## Authentication 

SSH supports two main types of authentication:

1. **Password authentication:**
	- The client sends a password (encrypted) to the server. 
	- The server verifes the password against its user database.
2. **Public key authentication** (recommended)
	- The client generates a key pair (private & public).
	- The public key is placed on the server (~/.ssh/authorized_keys)
	- During connection, the server challenges the client with a random encrypted message using the public key from `authorized keys` and the client proves ownership becasue only the private key can decrypt that challenge message. The client decrypts it locally and sends back the result (usually as a signature). The server then verfies the response matches what it expects, and if it does, access is granted. 
	- **Note:** this is a more secure method than passwords as it allows for features like passpharse-protected keys or hardware tokens like YubiKeys. Unlike a password (although encrypted) the private key never leaves the client machine.

## Encryption

SSH uses strong encryption algorithms as well as hashing to secure communication. Common algorithms include:
- **Symmetric encryption**, often call shared key encryption. Symmetric keys are used to encrypt the entire communication during a given SSH session. Both client and host create the secret key based on an agreed method. The key that is generated never leaves the scope  of the client and host. Additionally, the key is never transmitted between the client and the host machine. The two machines independently calculate the secret key. This secret token is specific to each session, and it is generated prior to cleitn authentication. Once the key is generated, all packets that move between the two machines are encrypted by the private key.
- **Asymmetric encryption** uses two seperate keys for encryption and decryption. These two keys are called *public* and *private* keys. Together they are called a *public-private key pair*. A public key can only be decrypted by the recipient who possesses the specific private key, and vice versa. To authenticate, the server sends a message that is encrypted using the clients public key, and that message can only be decrypted by the clients private key. This prossess happens completely automically and is not used to encrypt the entire SSH session.

## Hashing

Unlike the previous two forms of encryption, hashing is never meant to be decrypted. Hashing takes an input (like a password) and runs it through a mathematical function to produce a fixed-length string of characters called a hash. Becasue this function happens one-way, you cannot reverse the hash to get an original input. This makes it secure for passwords and data verification. 
