# Hush Line Documentation

## Table of Contents

1. [Introduction](#introduction)
2. [Intended Use](#intended-use)
3. [Architecture Overview](#architecture-overview)
4. [Installation](#installation)
5. [Security Measures](#security-measures)
6. [Configuration](#configuration)
7. [Maintaining and Updating](#maintaining-and-updating)
8. [E-Ink Displays](#e-ink-displays)
9. [Troubleshooting](#troubleshooting)
10. [Support and Contact](#support-and-contact)

## Introduction

Hush Line is a secure and anonymous tip line and suggestion box application. It allows users to receive messages securely from sources, colleagues, clients, or patients. The application is designed to be self-hosted, with PGP encryption, HTTPS, and a .onion address for Tor access, ensuring maximum privacy and security for both the sender and receiver.

This documentation provides an overview of the application's architecture, installation instructions, configuration details, maintenance procedures, troubleshooting tips, and support information.

## Intended Use

Hush Line is designed to be a self-hosted, secure, anonymous tip line and suggestion box that protects user privacy and message confidentiality. Its primary users and use cases include:

* **Journalists and newsrooms:** Hush Line provides a safe way for the public to leave confidential tips and allows journalists to securely communicate with sources.
* **Employers and boardrooms:** By offering an anonymous channel for colleagues to leave suggestions or report concerns, Hush Line can help build trust within the workplace.
* **Educators and school staff:** Hush Line serves as a secure platform for students to share information with trusted staff members, maintaining student anonymity and privacy.

Hush Line is especially important in areas with internet censorship, providing users a free and open-source platform to share sensitive information without fear.

Some specific use cases for Hush Line include:

* Providing sources with a trustworthy way to send information, ensuring their privacy is protected.
* Offering students a safe way to share information with school staff while protecting their identity.
* Allowing employees to report workplace abuse securely and privately, ensuring their identity is kept secret to avoid retaliation.
* Enabling students to report sensitive information anonymously to help bring about change without impacting their educational experience.
* Building trust within a team by ensuring that employees can share sensitive information without risking their careers.
* Facilitating communication with a Hush Line user even in countries with blocked access to the Tor Network and the original URL.

With its focus on security and privacy, Hush Line employs technologies such as PGP encryption, Tor, onion binding, HTTPS, and SMTP to ensure safe and reliable communication for its users.

### Using the app

Using Hush Line is simple and straightforward. Follow the steps below to send a secure, anonymous message through the platform:

1. **Obtain the Hush Line address:** The person hosting the Hush Line will provide you with their Hush Line address, which may be a regular web address (URL) or an onion address (.onion) for accessing via the Tor network.

2. **Access the Hush Line address:**
* If it is a regular web address (URL), open it in a web browser.
* If it is an onion address (.onion), you will need to use the Tor Browser to access it. Download and install the Tor Browser from the [official website](https://torproject.org) if you don't have it already.

3. **Compose your message:** Once you have accessed the Hush Line address, you will see a simple interface for composing your message. Verify the address of who you're sending the message tom, then type your message into the provided text box.

4. **Send the message:** After composing your message, click the "Submit" button to securely send the message. The platform will encrypt your message using the recipient's PGP public key, ensuring that only they can decrypt and read it.

By following these steps, you can safely and anonymously share sensitive information with the intended recipient through Hush Line.

## Architecture Overview

Hush Line is built using the following components:

* Python with Flask as the web application framework.
* PGP encryption using the PGPy library.
* Nginx as a reverse proxy server, handling HTTPS connections and forwarding requests to the Flask application.
* Certbot for obtaining SSL certificates from Let's Encrypt.
* Tor for onion service access, allowing the application to be accessed via a .onion address.
* Systemd service for managing the Hush Line application.

## Installation

To install Hush Line, simply run the script in the terminal with the following command:

### Tor + Public Web
```
curl -sSL https://raw.githubusercontent.com/scidsg/hush-line/main/install.sh | bash
```

### Tor-Only
```
curl -sSL https://raw.githubusercontent.com/scidsg/hush-line/main/install-tor-only.sh | bash
```

The script will guide you through the installation process, prompting you for the necessary information such as your domain name, email, and email server settings.

Before installation, ensure your domain's DNS settings are correctly pointing to your server's IP address.

Verify that Hush Line is running by accessing the application using the provided addresses.

## Security Measures

Hush Line takes several precautions to ensure the privacy and security of its users. Here are some of the key security measures in place:

1. **Message encryption:** The application uses PGP (Pretty Good Privacy) encryption to secure your messages. PGP is a data encryption method often used for encrypting, decrypting, and signing emails. Each message is encrypted using your public PGP key and can only be decrypted using your private PGP key.
2. **Secure transmission:** The application is configured to use HTTPS, a secure version of HTTP. HTTPS encrypts all the data transferred between the client (the person sending the message) and the server (your server).
3. **Email notifications:** The system sends you an encrypted email when receiving a new message. This ensures that even the notifications about incoming messages remain private.
4. **Tor network:** The application sets up a .onion domain, allowing access through the Tor network. The Tor network routes your data through several different servers around the world, making it very difficult for anyone to track the source or destination of the data.
5. **Private server:** The application is set up on your own server. This means you have full control over the data, and there's no third-party involved who could potentially access the data.
6. **Privacy-focused logging:** Nginx, the web server used by the application, is configured to preserve privacy in its logging. IP addresses are anonymized, and only the country code of the client is logged.
7. **Automatic updates:** The application configures unattended-upgrades, which automatically installs security updates. This ensures that your server stays up-to-date with the latest security patches.
8. **Restricted headers and permissions:** The Nginx configuration includes several headers designed to increase the security of the application, like preventing the app from being embedded into an iframe (X-Frame-Options: DENY), instructing the browser only to use HTTPS (Strict-Transport-Security) and not allowing third-party content to load (Content-Security-Policy: default-src 'self').
9. **Secure storage of messages:** Messages are stored in an encrypted format on the server. The server doesn't store any information about who sent the message, preserving the anonymity of your sources.
10. **Secure email transmission:** The application uses SMTP over SSL/TLS for sending emails, ensuring that the emails are securely transmitted over the network.

By implementing these security measures, Hush Line ensures that users can confidently share sensitive information without fear of compromising their privacy or security

## Configuration

During the installation process, the script configures the following components:

* Systemd service for managing the Hush Line application.
* Tor hidden service for .onion access.
* Nginx reverse proxy server for SSL termination and forwarding requests to the Flask application.
* Certbot for SSL certificate management.
* Automatic updates via unattended-upgrades.

### Recommended Email Setup

For the email service configuration during Hush Line installation, we recommend using a Gmail account with a one-time password. This approach enhances security, as one-time passwords are valid only for a single login session. Please note that Hush Line stores email passwords in plaintext; however, your messages are encrypted, so Google won't be able to read their contents.

#### Setting up Gmail with One-Time Passwords

If you don't have a Gmail account, create one at gmail.com.

##### Enable 2-Step Verification:

1. Sign in to your Google Account.
2. Go to the 2-Step Verification page.
3. Click on "Get Started."
4. Follow the prompts to enable 2-Step Verification.

##### Generate an App Password:

1. Go to the App Passwords page.
2. Click on "Select App" and choose "Mail."
3. Click on "Select Device" and choose "Other."
4. Enter a descriptive name (e.g., "Hush Line") and click on "Generate."
5. A 16-character password will be generated. Save this password, as you'll need it during Hush Line installation.

#### Configuring Hush Line with Gmail

During the Hush Line installation process, when prompted for email configuration:

* Enter your Gmail address
* Enter the one-time password you generated in the previous section
* SMTP server address: smtp.gmail.com
* SMTP server port: 465

By following these steps, you'll ensure a more secure email configuration for your Hush Line instance.

## Maintaining and Updating

**Regular updates:** The unattended-upgrades package is configured to automatically update your server, including security updates. No manual intervention is needed.

**SSL certificate renewal:** The installation script sets up a cron job to automatically renew the SSL certificates using Certbot.

## E-Ink Displays

In this section, we'll discuss how to set up an e-ink display for your Hush Line project. The e-ink display will show the status of your Hush Line instance, onion address, and QR code for easy access to the service. The script provided will install necessary packages and configure the Raspberry Pi for proper communication with the e-ink display.

![hush-line-display](https://user-images.githubusercontent.com/28545431/236598264-728eb43a-d23c-4dac-a13d-7487e3fe88ea.png)

### Setup

To set up the e-ink display, exectue the following command in your terminal:
```
curl -sSL https://raw.githubusercontent.com/scidsg/tools/main/hushline-eink-rpi-display.sh | bash
```

The script will install the required packages, configure the SPI interface, set up the Waveshare e-Paper library, and create necessary Python scripts for managing the e-ink display. It will also download a splash screen image and enable a service to clear the display before shutdown.

Once the setup script has finished running, your Raspberry Pi will automatically reboot for the changes to take effect.

### E-Ink Display Functionality

The e-ink display will show:

* The status of your Hush Line instance (running or not running)
* Onion address of your Hush Line instance
* QR code to access your Hush Line instance
* PGP public key information (name, email, key ID, and expiration date)

The script will refresh the e-ink display every minute to provide up-to-date information.

![display](https://user-images.githubusercontent.com/28545431/236600758-f1acc31a-b8a8-408e-b77f-ca62b593b6b5.png)

### E-Ink Display Management

The provided script includes two Python scripts for managing the e-ink display:

**display_status.py:** Displays the status, onion address, QR code, and PGP public key information on the e-ink display.

**clear_display.py:** Clears the e-ink display.

These scripts are automatically run on boot and before shutdown, respectively. You can also run them manually if needed.

## Troubleshooting

If Hush Line is not running, check the status using the following command:
```
systemctl status hush-line.service
```

If there are any issues with Nginx, verify the configuration using the following command:

```
sudo nginx -t
```

Check the logs for Hush Line, Nginx, and Tor for any error messages or clues:

**Hush Line:** /var/log/syslog

**Nginx:** /var/log/nginx/error.log

**Tor:** /var/log/tor/log

## Support and Contact

If you have any questions, feedback, or need assistance, please contact us at:

**Website:** https://scidsg.org

**Email:** support@scidsg.org

