# Deploy on Ubuntu

The goal of this tutorial is to help people deploy their admin backend to an Ubuntu server.

#### Connect to your Ubuntu server using SSH <a href="#connect-to-your-ubuntu-server-using-ssh" id="connect-to-your-ubuntu-server-using-ssh"></a>

Before starting anything, you have to make sure you're able to connect to your server using SSH.

Warning: Permanently added 'ec2-18-204-18-81.compute-1.amazonaws.com,18.204.18.81' (ECDSA) to the list of known hosts.

Welcome to Ubuntu 18.04.1 LTS (GNU/Linux 4.15.0-1021-aws x86\_64)

#### Copy the code of your admin backend to your remote server <a href="#copy-the-code-of-your-admin-backend-to-your-remote-server" id="copy-the-code-of-your-admin-backend-to-your-remote-server"></a>

There are many ways to copy the code of your admin backend to a remote server. For example, you can use `rsync` command, or use a versioning system like `git`.

We **strongly advise** versioning the code of your admin backend using **git** and hosting it to a **private repository** on Github, Bitbucket, Gitlab, or other providers.

> **rsync** is a utility for efficiently transferring and synchronizing files across computer systems, by checking the timestamp and size of files. It is _commonly_ found on Unix-like systems and functions as both a file synchronization and file transfer program.
>
> Rsync is typically used for synchronizing files and directories between two different systems. (source: [wikipedia](https://en.wikipedia.org/wiki/Rsync))

The syntax used is `rsync OPTIONS SOURCE TARGET`.

rsync -avz -e "ssh -i \~/.ssh/aws.pem -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null" --exclude=node\_modules --exclude=.git --progress QuickStart \[email protected]:\~/

In the example above, we use an SSH connection to transfer the file and we connect to the remote server using an identity\_file (a private key).

| Option            | Description                            |
| ----------------- | -------------------------------------- |
| -a                | archive mode; same as -rlptgoD (no -H) |
| -v                | increase verbosity                     |
| -z                | compress file data during the transfer |
| -e                | specify the remote shell to use        |
| --exclude=PATTERN | exclude files matching PATTERN         |
| --progress        | show progress during transfer          |

Once done, you can find the code of your admin backend on the home directory of your remote server.

\-rw-r--r-- 1 ubuntu ubuntu 1386 Oct 22 08:11 app.js

\-r-------- 1 ubuntu ubuntu 1692 Oct 23 12:51 aws.pem

drwxr-xr-x 2 ubuntu ubuntu 4096 Oct 12 10:19 bin

\-rw-r--r-- 1 ubuntu ubuntu 5126311 Oct 12 11:20 database.dump

drwxr-xr-x 2 ubuntu ubuntu 4096 Oct 19 11:49 forest

drwxr-xr-x 2 ubuntu ubuntu 4096 Oct 19 12:22 models

\-rw-r--r-- 1 ubuntu ubuntu 69568 Oct 22 07:30 package-lock.json

\-rw-r--r-- 1 ubuntu ubuntu 717 Oct 22 07:30 package.json

drwxr-xr-x 2 ubuntu ubuntu 4096 Oct 12 10:19 public

drwxr-xr-x 2 ubuntu ubuntu 4096 Oct 22 07:48 routes

drwxr-xr-x 2 ubuntu ubuntu 4096 Oct 19 11:53 serializers

drwxr-xr-x 2 ubuntu ubuntu 4096 Oct 19 11:55 services

First, you need to initialize a git repository for the code of your admin backend. From the directory of your admin backend, simply run:

Then, you can add all the files and create your first commit.

git commit -am "First commit"

Finally, you can add your git remote and push the code on your favorite platform. To do so, **first**, create a new QuickStart repository on your GitHub account. **Then** run the following command after changing `YourAccount` to your account name:

git push -u origin master

Now, you can connect to your remote server using SSH and clone the repository using the HTTPS method.

git clone https://github.com/YourAccount/QuickStart.git

Cloning into 'QuickStart'...

remote: Enumerating objects: 34, done.

remote: Counting objects: 100% (34/34), done.

remote: Compressing objects: 100% (21/21), done.

remote: Total 34 (delta 7), reused 34 (delta 7), pack-reused 0

Unpacking objects: 100% (34/34), done.

That's it. Your admin backend's code is available on your remote server.

\-rw-rw-r-- 1 ubuntu ubuntu 1386 Oct 23 13:42 app.js

drwxrwxr-x 2 ubuntu ubuntu 4096 Oct 23 13:42 bin

\-rw-rw-r-- 1 ubuntu ubuntu 5126311 Oct 23 13:42 database.dump

drwxrwxr-x 2 ubuntu ubuntu 4096 Oct 23 13:42 forest

drwxrwxr-x 2 ubuntu ubuntu 4096 Oct 23 13:42 models

\-rw-rw-r-- 1 ubuntu ubuntu 69568 Oct 23 13:42 package-lock.json

\-rw-rw-r-- 1 ubuntu ubuntu 717 Oct 23 13:42 package.json

drwxrwxr-x 2 ubuntu ubuntu 4096 Oct 23 13:42 public

drwxrwxr-x 2 ubuntu ubuntu 4096 Oct 23 13:42 routes

drwxrwxr-x 2 ubuntu ubuntu 4096 Oct 23 13:42 serializers

drwxrwxr-x 2 ubuntu ubuntu 4096 Oct 23 13:42 services

First, you have to make sure you have Node.js and NPM correctly installed on your server.

sudo apt install nodejs npm

Then, you will be able to install all the dependencies listed on the package.json file.

This step is **optional** if you already have a running database.

First, you need to install PostgreSQL:

sudo apt-get install postgresql postgresql-contrib

Then, you will be able to connect to the database server:

psql (10.5 (Ubuntu 10.5-0ubuntu0.18.04))

Now, we can export the database from your local environment (your computer) to import it to your Ubuntu server.

For security reasons, we will not allow remote connections to this database. This is why transfer the database dump to the remote server using `rsync.`

PGPASSWORD=secret pg\_dump -h localhost -p 5416 -U forest forest\_demo --no-owner --no-acl -f database.dump

rsync -avz -e "ssh -i \~/.ssh/aws.pem -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null" --progress database.dump \[email protected]:\~/

Then, we will create a new DB user and schema from the remote server:

postgres=# CREATE USER forest WITH ENCRYPTED PASSWORD 'secret';

postgres=# CREATE DATABASE forest\_demo;

postgres=# GRANT ALL PRIVILEGES ON DATABASE forest\_demo TO forest;

And finally, import the dump:

PGPASSWORD=secret psql -U forest -h 127.0.0.1 forest\_demo < database.dump

That's it, your database is now fully imported.

PGPASSWORD=secret psql -U forest -h 127.0.0.1 forest\_demo

psql (10.5 (Ubuntu 10.5-0ubuntu0.18.04))

Schema | Name | Type | Owner

\--------+---------------------+----------+----------

public | Companies\_id\_seq | sequence | postgres

public | addresses | table | postgres

public | addresses\_id\_seq | sequence | postgres

public | appointments | table | postgres

public | appointments\_id\_seq | sequence | postgres

public | companies | table | postgres

public | customers | table | postgres

public | customers\_id\_seq | sequence | postgres

public | deliveries | table | postgres

public | deliveries\_id\_seq | sequence | postgres

public | documents | table | postgres

public | documents\_id\_seq | sequence | postgres

public | orders | table | postgres

public | orders\_id\_seq | sequence | postgres

public | products | table | postgres

public | products\_id\_seq | sequence | postgres

public | transactions | table | postgres

public | transactions\_id\_seq | sequence | postgres

#### Export the environment variables <a href="#export-the-environment-variables" id="export-the-environment-variables"></a>

You must export the environment variables `FOREST_ENV_SECRET` `FOREST_AUTH_SECRET` and `DATABASE_URL`. To do so, open and edit the file `/etc/environment`:

The `FOREST_ENV_SECRET` and `FOREST_AUTH_SECRET` environment variables will be given by Forest after creating a production environment from the interface. See how to get them here.

sudo vim /etc/environment

PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games"

FOREST\_ENV\_SECRET=2417520743be37a9c5af198c018e0ddee9b7c41de1ccb8e76c9d027faa74059e

FOREST\_AUTH\_SECRET=Piq7a9Kv5anLbK4gj81rirsLhfaJ0pdL

Then, you can restart your server to take these new variables into account or simply type:

for env in $( cat /etc/environment ); do export $(echo $env | sed -e 's/"//g'); done

From your admin backend's directory, simply type:

🌳 Your back office API is listening on port 3000 🌳

🌳 Access the UI: http://app.forestadmin.com 🌳

Congrats, your admin backend is now running on production. But we strongly advise you to continue following the next steps. If you chose not to do it, you can go back to your Forest interface to create a production environment. Check out here how to do it.

The admin backend is by default listening on port **3310**. Be sure you authorized the inbound traffic on this port or set up a web server (like NGINX) as a [Reverse Proxy Server](broken-reference) to use the port **80.**

#### Manage Application with PM2 <a href="#manage-application-with-pm2" id="manage-application-with-pm2"></a>

> PM2 is a Production Runtime and Process Manager for Node.js applications with a built-in Load Balancer. It allows you to keep applications alive forever, to reload them without downtime and facilitate common Devops tasks. source: [npmjs/pm2](https://www.npmjs.com/package/pm2)​

**Run your admin backend using PM2**

#### (Optional) Set Up Nginx as a Reverse Proxy Server <a href="#optional-set-up-nginx-as-a-reverse-proxy-server" id="optional-set-up-nginx-as-a-reverse-proxy-server"></a>

Now that your admin backend is running and listening on localhost:3310, we will set up the Nginx web server as a reserve proxy to allow your admin panel's users access it.

To do so, edit (with sudo access) the file located `/etc/nginx/sites-available/default` and replace the existing section `location /` by this one:

/etc/nginx/sites-available/default

proxy\_pass http://localhost:3000;

proxy\_set\_header Upgrade $http\_upgrade;

proxy\_set\_header Connection 'upgrade';

proxy\_set\_header Host $host;

proxy\_cache\_bypass $http\_upgrade;

sudo systemctl restart nginx

That's it, your admin backend is now listening on the port **80**. Make sure your firewall allows inbound traffic from this port.

Once you've completed the above steps, it does **not** mean your project is deployed to production on Forest Admin. To deploy to production, check out this section.
