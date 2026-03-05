# Hostinger VPS SSH Access Guide (Windows)

This guide will walk you through generating an SSH key, adding it to your Hostinger VPS, and connecting securely.

## Step 1: Generate an SSH Key Pair

On your Windows machine, open **PowerShell** or **Command Prompt** and run:

```powershell
ssh-keygen -t ed25519 -C "your_email@example.com"
```

1.  **Enter file in which to save the key:** Press `Enter` to use the default location (`C:\Users\YourName\.ssh\id_ed25519`).
2.  **Enter passphrase:** (Optional) Enter a password for the key itself, or press `Enter` to leave it empty for no password.

## Step 2: Copy Your Public Key

You need to copy the content of the **public** key (`id_ed25519.pub`) to paste it into Hostinger.

Run this command in PowerShell to display the key:

```powershell
Get-Content $HOME\.ssh\id_ed25519.pub
```

Select the entire line (starting with `ssh-ed25519`) and copy it.

## Step 3: Add the Key to Hostinger hPanel

1.  Log in to your **[Hostinger hPanel](https://hpanel.hostinger.com/)**.
2.  Navigate to **VPS** -> **Manage** (for your specific VPS).
3.  On the left sidebar, go to **Settings** -> **SSH Keys**.
4.  Click **Add SSH Key**.
5.  **Name:** Give it a name (e.g., "Windows-Local").
6.  **Key:** Paste the public key you copied in Step 2.
7.  Click **Add SSH Key**.

## Step 4: Connect to Your VPS

Now you can connect using the `ssh` command. You will need your **VPS IP Address** and the **Username** (standard is usually `root` or the specific user you created).

In PowerShell/Command Prompt:

```powershell
ssh username@your_vps_ip
```

> [!TIP]
> If you are using a user other than `root`, ensure that user has SSH access enabled in the VPS settings.

---

## Step 5: Copy Files to Your VPS (Deployment)

Once you have SSH access, you can copy your build files (e.g., from a `dist` or `build` folder) to your server's web directory (usually `public_html` or `htdocs`).

### Option A: Using SCP (Simple Copy)

Use this for quick, one-off transfers.

```powershell
# Format: scp -r local_folder username@vps_ip:remote_path
scp -r ./dist/* root@your_vps_ip:/home/user/public_html/
```

### Option B: Using Rsync (Efficient Sync - Recommended)

`rsync` only copies changed files and is much faster for repeated deployments.

```powershell
# Format: rsync -avzP local_folder/ username@vps_ip:remote_path
rsync -avzP ./dist/ root@your_vps_ip:/home/user/public_html/
```

> [!NOTE]
> **Finding your remote path:** Most Hostinger VPS setups use `/home/username/public_html/` or `/var/www/html/`. You can find the exact path by connecting via SSH (`Step 4`) and running `pwd`.

---

## Troubleshooting

- **Permission Denied (publickey):** Ensure you added the **public** key (.pub) to Hostinger, not the private one.
- **Connection Timeout:** Check if your VPS firewall allows port 22 (standard SSH).
- **Wrong Path:** Ensure the target directory on the VPS exists before running `scp` or `rsync`.
