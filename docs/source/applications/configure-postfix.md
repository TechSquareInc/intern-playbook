# 📨 Configure Postfix

*Confgiure Postfix using Gmail as a relay.*

---

## What is Postfix?
Postfix is an open source software that routes and delivers email. One potential application for its use is in sending emails directly through the command line. Relevently, it is also possible to set up Postfix to send email alerts connected to server monitoring software like `checkmk`.

Postfix is designed with security in mind, though its installation can be tricky depending on customization needs. A popular choice is to set up Postfix to use Gmail as a relay for sending emails.

## Installation and Configuration
There have been some slight changes to how to configure Gmail as the relay recently because Google has depricated its "insecure apps" option. In order to allow sign-in from Gmail using Postfix, you will need to enable "less secure apps" in Google's security settings, and create an App Password. Before this, you will need to make sure 2FA is enabled.

**What's an App Password?**

**App Passwords** are a way to allow your application to "Sign in with Google." When Google does not allow the option to "Sign in with Google" you can either:
- switch to a more secure app or device
- use app passwords

> **Important:**
> To create an app password, you need 2-Step Verification on your Google Account. To enable 2FA, go to your Google accounts [security settings](https://myaccount.google.com/security) and turn on "2-Step Verification".

- Once 2FA is configure, on the same security settings page you will see the "Less Secure Apps" feature is disabled by default. Toggle this setting "on".

- Now that 2FA is enabled and "less secure apps" is turned on, you can create an **app password** for Postfix. While you are still signed in to your Google account, follow this link to [create and manage your app passwords](https://myaccount.google.com/apppasswords).

- On the app passwords page, enter a name for the application you are creating a password for, in this case "Postfix". A 16-digit passcode will be generated. Place this passcode in a secure location for now, as we will need it later on while configuring Postfix.

### Installation
1. It is required to install Postfix as the root user. Switch to root and perform systme updates:
```bash
su - root
yum update
```

2. Install Postfix using the command:
```bash
yum install postfix
```

3. Start the Postfix service using the command:
```bash
systemctl start postfix
```

4. To make sure Postfix starts automatically after a server reboot, run the command:
```bash
systemctl enable postfix
```

5. By defualt, Postfix listens on port 25 for incoming mail. If you're running a firewalll on your server, make sure to open port 25 by running the command:
```bash
firewall-cmd --permanent --add-port=25/tcp
firewall-cmd --reload
```

6. You can test the installation by sending an email to a valid email address from your command line using the mail command:
```bash
yum install s-nail
echo "This is a test email" | mail -s "Test Email" recipient@example.com
```

> **Note:** Check your spam folder, the email will come from `root` and appear from the sender `<root@localhost.localdomain>`. This is a good sign. It means postfix has been succesfully installed and is working as expected.

Next, let's configure the application to sign-in using your Gmail account.

### Configure
1. To configure your Gmail account, install the `cyrus-sasl` packages on the system.
```bash
sudo yum install cyrus-sasl-*
```

2. Add/change the following parameters in the `/etc/postfix/main.cf` file:
```bash
relayhost = [smtp.gmail.com]:587
smtp_sasl_auth_enable = yes
smtp_tls_security_level = encrypt
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
smtp_sasl_tls_security_options = noanonymous
smtp_tls_policy_maps = hash:/etc/postfix/tls_policy
```
and comment out the line that says
```bash
smtp_tls_security_level = may
```

3. Add Gmail's username and the app password you just created in the `/etc/postfix/sasl_passwd` file:
```bash
[smtp.gmail.com]:587	<user>@gmail.com:<app-password>
```

4. Configure encryption in `/etc/postfix/tls_policy`:
```bash
[smtp.gmail.com]:587 encrypt
```

5. Create the database of files:
```bash
chmod 600 /etc/postfix/sasl_passwd
postmap /etc/postfix/sasl_passwd
postmap /etc/postfix/tls_policy
```

6. Restart the `postfix` service:
```bash
systemctl restart postfix
```

7. Send a test and verify the status:
```bash
echo "mailtest" | mail -s "mailtest" <user>@<domain.com>
```

8. If successful, you will recieve an email in your inbox from your gmail domain.

## Resources
- [Postfix Official Documentation](https://www.postfix.org/documentation.html): Everything Postfix explained.
- [Sign-in with App Passwords](https://support.google.com/mail/answer/185833?hl=en): A google help center guide to app passwords.
- [A Comprehensive Guide to Connect Postfix to Gmail](https://www.systoolsgroup.com/add/postfix-to-gmail-account/?srsltid=AfmBOopprwRvW4esdO2xmgbWs9XG6gIvAkKxQFCEouka6jc8jizHtoFE): An updated resource for confgiruing Postfix (Debian environment).
- [How to Configure Gmail Server as a Relayhost in Postfix](https://access.redhat.com/solutions/3201002): An updated resource for configuring Postfix (REHL environment).
- [Create and Manage Your App Passwords](https://myaccount.google.com/apppasswords): Quick link to creating app passwords.
- [Google Security Settings](https://myaccount.google.com/security): Your Google account's security settings page.


