# Docker images

This repository contains Dockerfile-s and corresponding docker-compose.yml files.

## Aquila CMS

Aquila CMS a small, user friendly content management system. You can find the official github
repository at

    https://www.github.com/AquilaCMS/AquilaCMS

It can be run locally on your host machine, but this repository provides a Dockerfile and docker-compose.yml for
containerized deployment. MongoDB is required for Aquila CMS, and is configured in docker-compose.yml. For more
information, please refer to the official README.md file.

### Mail server configuration

For a smoother experience with Aquila CMS, I recommend configuring mail server settings in the admin panel.
One effective approach is to use your Gmail account by generating a new App Password and configuring the mail
settings in the admin panel.

#### Step 1: Set Up Gmail Account for SMTP
        
Enable Two-Factor Authentication (2FA):
Go to https://myaccount.google.com/security.
Under Sign-in to Google, click 2-Step Verification and follow the steps to enable it (e.g., using your phone for verification).
2FA is required to generate an App Password.
        
- Generate an App Password:

    In the same Security section, find App Passwords (you may need to search for it or scroll down).
    Click Select app > Other (Custom), and name it (e.g., “AquilaCMS”).
    Click Generate to get a 16-character password (e.g., abcd efgh ijkl mnop).
    Copy this password securely; you’ll use it instead of your regular Gmail password.

    Verify Gmail Address:

    Confirm the Gmail address you’re using (e.g., yourname@gmail.com) is correct and matches the account where you generated the App Password.

#### Step 2: Configure Aquila CMS for Gmail SMTP
        
- Aquila CMS typically allows email configuration through environment variables or a configuration file. Since you’re running in Docker, environment variables are the most Docker-friendly approach.

    Update Email Configuration:
        
    Aquila CMS uses nodemailer under the hood, and its email settings are often defined in config/env.js or overridden via environment variables like SMTP_HOST, SMTP_PORT, SMTP_USER, and SMTP_PASS.
    For Gmail, use the following settings:

        SMTP Host: smtp.gmail.com
        SMTP Port: 587 (for TLS)
        SMTP User: yourname@gmail.com
        SMTP Pass: Your 16-character App Password from Step 1
        SMTP Secure: false (since port 587 uses STARTTLS)