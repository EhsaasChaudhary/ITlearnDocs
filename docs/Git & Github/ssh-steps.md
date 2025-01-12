# How to Create an SSH Key for GitHub and Save it

## 1. Generate the SSH Key Pair
1. **Open a terminal.**
2. Run the following command to create a new SSH key pair:
   
   Recommended:
   ```bash
   ssh-keygen -o
   ```

   Alternative (with custom options):
   ```bash
   ssh-keygen -o -t rsa -b 4096 -C "your_email@example.com"
   ```

## 2. Choose a Location to Save the Key
- When prompted, you can specify a custom location for the key file or press **Enter** to use the default location (`~/.ssh/id_rsa`).

## 3. Enter a Passphrase (Optional)
- You will be asked to enter a passphrase to secure the key. This is optional; press **Enter** for no passphrase.

## 4. Locate the SSH Key
- Navigate to the `.ssh` directory (default location) using your terminal or file explorer.
- Open the `.pub` file (e.g., `id_rsa.pub`) located in the `.ssh` folder.
- Copy the content of the `.pub` file, starting with `ssh-`.

## 5. Add the SSH Key to GitHub
1. Log in to your GitHub account.
2. Go to **Settings**:
   - Click on your profile picture (top-right corner) > **Settings** > **SSH and GPG Keys**.
3. Click **New SSH Key**.
4. Add a title (e.g., `EC Laptop`) and paste the public key into the "Key" field.
5. Click **Add SSH Key**.

## 6. Verify the SSH Connection
Run the following command to verify your SSH connection to GitHub:

```bash
ssh -T git@github.com
```

- You should see a message like this:
  ```bash
  Hi EhsaasChaudhary! You've successfully authenticated, but GitHub does not provide shell access.
  ```
  ---
