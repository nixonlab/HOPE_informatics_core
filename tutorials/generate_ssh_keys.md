# Tutorial: Generating an SSH Key Using the ED25519 Protocol

## Introduction

SSH keys are a pair of cryptographic keys (one public "`.pub`", one private) used for secure access to remote servers. They are an alternative to passwords and provide stronger security because they are nearly impossible to guess or crack.

The ED25519 protocol is a modern and secure algorithm for generating SSH keys. There are other older algorithms you might encounter (e.g. "RSA") but ED25519 is better and uses smaller keys.

This guide will walk you step-by-step through generating an SSH key using the ED25519 protocol. 


---

## Step 1: Understand the Requirements

Before we start, ensure you have:
1. **A terminal or command-line interface**: This is where you'll type commands.
   - On **macOS** and **Linux**, a terminal app is included by default.
2. **An SSH client installed**: Most modern operating systems include one.

---

## Step 2: Open the Terminal

- **macOS**:  
  Press `Cmd + Space`, type "Terminal," and press Enter.
- **Linux**:  
  Open your application menu and look for "Terminal," or press `Ctrl + Alt + T`.

---

## Step 3: Generate the SSH Key

1. **Run the following command** in the terminal:
   ```bash
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```
   
Replace `your_email@example.com` with your actual email address. This email serves as a label to identify the key.

2. Specify the location to save the key: You’ll see a prompt:

```
Enter file in which to save the key (/home/your-username/.ssh/id_ed25519):
```
- Press Enter to save it in the default location (`~/.ssh/id_ed25519`)
   
3. Set an empty passphrase: You'll be prompted

```
Enter passphrase (empty for no passphrase):
```

- leave it empty and press Enter. 
- again, leave it empty and press Enter.
   
4. Verify the Key was created:

If successful, the output will look similar to this:

```
Your identification has been saved in /home/your-username/.ssh/id_ed25519.
Your public key has been saved in /home/your-username/.ssh/id_ed25519.pub.
The key fingerprint is:
SHA256:abcdefgh12345678abcdefgh12345678abcdefgh1234 your_email@example.com
The key's randomart image is:
+--[ED25519 256]--+
|     ..          |
|   .::..         |
|  . o==.         |
|   oE+o+ .       |
|   ....          |
+----[SHA256]-----+

```

Now you will have two files in your `~/.ssh` directory : 
   
- The private key is stored in id_ed25519 (**never share this file!**).
- The public key is stored in id_ed25519.pub (this can be shared when setting up access).

5. Add the Public Key to Your Services:

While you already have an account in the cluster, we need you to provide your ssh public key to grant you secure access. 

- View your **public key**

```bash
cat ~/.ssh/id_ed25519.pub
```

There will be an output that looks something like this: 

```
ssh-ed25519 AAAAC3...restofyourkey... your_email@example.com

```

Highlight this output in the terminal and copy it (Ctrl + C on Linux, Cmd + C on macOS).

Send your public key to hreyesgopar@northwell.edu. 

Congratulations, You’ve successfully generated an SSH key using the ED25519 protocol. You'll be able to test your connection to the server very soon.

   
   
   
