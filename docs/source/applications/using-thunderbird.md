# Using Thunderbird

*Thunderbird is a free and open-source email client developed by Mozilla. It allows you to manage multiple email accounts from your desktop, supporting protocols like IMAP, POP3, and SMTP. Thunderbird can be used to: read and send emails, manage multiple accounts, organize emails into folders, work offline with cached messages, and use calander and task add-ons.*

---

## Step 1: Install Thunderbird
```bash
sudo yum update
sudo yum install thunderbird
```

## Step 2: Enable IMAP in Gmail

1. Log into Gmail
2. Click the gear icon -> See all settings
3. Go to the Forwarding and POP/IMAP tab
4. Under IMAP Access, select Enable IMAP
5. Save changes

## Step 3: Add Gmail Account to Thunderbird

1. Open Thunderbird.
2. Go to Account Settings->Add Mail Account, or use Thunderbirds startup wizard.
3. Enter your:
	- Name
	- Email
	- Password
4. Click Continue, Thunderbird will auto-detect Gmail settings.
5. Click Done. If prompted to sign in via your browser, follow the Google sign-in process.

## Step 4: Test Your Setup
- Confirm that Thunderbird shows your Gmail inbox.
- Send a test email to verify outgoing email works.
- Thunderbird will sync folders.

## Optional Configuration
- Use filters and folders to sort emails
- Add the Lightning calendar add-on
- Adjust sync settings to reduce disk usage
- Backup profile using Thunderbird's profile manager

---
## Resources
- [Thunderbird Offical Site](https://www.thunderbird.net/en-US/)
- [Thunderbird Gmail Setup Docs](https://support.mozilla.org/en-US/kb/thunderbird-and-gmail)
- [Gmail IMAP Settings](https://support.google.com/mail/answer/7126229)
- [Thunderbird Add-ons](https://addons.thunderbird.net/en-US/thunderbird/)
- [Installing Thunderbird on Fedora, RHEL](https://www.if-not-true-then-false.com/2011/install-thunderbird-on-fedora-centos-and-red-hat-rhel/)
