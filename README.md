# <ins>**2420 Week 12 Lab**</ins>

This repo contains an html document file and a server block file accommodated for Nginx.

In this README, you will be building and setting up your own web server, and presenting your document onto a web browser.

You will be using DigitalOcean droplets and Nginx web server to display your content and your application to the browser.

---

## <ins>**1. Table of Contents**</ins>

- [**2420 Week 12 Lab**](#2420-week-12-lab)
  - [**1. Table of Contents**](#1-table-of-contents)
  - [**2. Set B Members**](#2-set-b-members)
  - [**3. Technologies Used**](#3-technologies-used)
  - [**4. Prerequisites**](#4-prerequisites)
  - [**5. Tutorial**](#5-tutorial)
    - [**Install Nginx**](#install-nginx)
    - [**Creating an HTML Document**](#creating-an-html-document)
    - [**Creating Nginx Server Block File**](#creating-nginx-server-block-file)

---

## <ins>**2. Set B Members**</ins>

Nazira Fakhrurradi (A01279940)  
Aaron Matthew Arcalas

---

## <ins>**3. Technologies Used**</ins>

- Bash
- Windows Subsystem for Linux (WSL) - Ubuntu
- DigitalOcean (DO)
- Nginx
- Git
- HTML
- Windows Terminal or Powershell

---

## <ins>**4. Prerequisites**</ins>

- You have `WSL Ubuntu` installed and have created a regular user inside it.
- You have created a DO droplet `web-one` server and have created a regular user.
- You can connect via ssh from `WSL` to regular user in `web-one`.
- You can connect via ssh from `Windows Terminal` or `Powershell` to regular user in `WSL`.

---

## <ins>**5. Tutorial**</ins>

### <ins>**Install Nginx**</ins>

> **Note:** You may need to open your Terminal as Administrator.

From your Windows Terminal or Powershell, connect to `WSL`, then connect to `web-one`.

1. Update any packages currently installed on `web-one`:

```
username@web-one:~$ sudo apt update
```

![apt update output](images/apt-update.png "apt update")

2. Upgrade currently installed packages:

```
username@web-one:~$ sudo apt upgrade
```

![apt upgrade output](images/apt-upgrade.png "apt upgrade")

3. To confirm changes, press `tab` and then `ENTER`:

![confirm changes](images/package-config.png "confirm changes")

4. Finally, install `nginx`:

```
username@web-one:~$ sudo apt install nginx
```

![apt install nginx](images/install-nginx.png "install nginx")

> **Note:** If you are prompted to restart services, press `tab` and then `ENTER`.

5. Check if `nginx` is successfully installed:

![check nginx](images/list-installed.png "list nginx")

---

### <ins>**Creating an HTML Document**</ins>

Within `WSL`, you will create an HTML file in a logical directory. You will be sending this file to `web-one`, eventually.

1. Create an `index.html` file with the following content:

```
username@DESKTOP:/mnt/c/Users/...$ vim index.html
```

```
<!DOCTYPE html>
<html lang="en">
<html>
    <head>
    <meta charset="UTF-8" />
        <title>Example Site for 2420</title>
    </head>
    <body>
        <h1>Success!</h1>
        <h2 style="color: red;">All your internets are belong to us!</h2>
    </body>
</html>
```

2. Check the file's content:

![check index html](images/index-html.png "cat index html")

---

### <ins>**Creating Nginx Server Block File**</ins>

The server block file is used to serve your HTML document that you created from [**Creating an HTML Document**](#creating-an-html-document).

1. Within `WSL`, create a text file with your DO droplet's IP Address as the name:

```
username@DESKTOP:/mnt/c/Users/...$ vim 137.184.13.89
```

2. Write the following content to the file:

> **IMPORTANT:** `root` directive should have your server's IP Address to it: `/var/www/<IP_ADDRESS>/html;`
> 
> `server_name` directive should also have your server's IP Address: `<IP_ADDRESS>;`

```
server {
        listen 80;
        listen [::]:80;

        root /var/www/137.184.13.89/html;
        index index.html;

        server_name 137.184.13.89;

        location / {
                try_files $uri $uri/ =404;
        }
}
```

1. Check the file's content:

![check server block](images/server-block.png)

