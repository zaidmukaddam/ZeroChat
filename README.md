<h1 align="center">
ZeroChat 
</h1>

<p align="center">

A live web chat. No client-side javascript, cookies, accounts, or `<meta http-equiv="refresh">` tags.

Instead, your browser never finishes loading the whole page, and downloads messages as they are posted by others.

Authentification is done with a password/tripcode system using PBKDF2 hashes.

## Try it by visiting [zerochat.tech](https://zerochat.tech/)

**It's easy to self-host, and simple to use.** Developed with a security-first mentality.

#### Username and Password? But no accounts required!
- You can login using a handle of your choosing, and enter a "passcode" which is hashed into a unique "tripcode" for your passcode only
- A passcode is like a password, but no accounts are needed to enter a room, everyone just proves who they are by their tripcode

#### Rooms
- Choose from a preselected list of "public" rooms that are advertised on the front page by clicking the Room textbox twice. 
- Or, enter any name you want for your room, and you'll "tune" into it like a radio frequency.

You can share a link with `/roomName` at the end of the URL to have your friends join that room.

Wondering [how it's a live chat without javascript](https://zaidmukaddam.biz/writing/stateful-http)?

## Running & Dependencies

This project requires NodeJS, unless you download one of the [releases](https://github.com/zaidmukaddam/ZeroChat/releases) (Supported only on windows).

### Running ZeroChat on Windows

Take a look at the [releases](https://github.com/zaidmukaddam/ZeroChat/releases) for executable binaries if you just want to run the chat server.

If you want to tweak the program and run the source code on Windows without docker, follow along with the [steps to self host](#self-hosting-without-docker) below!

### Self Hosting

All you need is `node`, which comes with `npm`!

**For Linux or Mac**: Run the following to install the wonderful **[n](https://github.com/tj/n)** NodeJS version manager, then install NodeJS v12.0.0:

```bash
curl -L https://git.io/n-install | bash
n 12.0.0
npm --version
```

**For Windows**: [Download and install NodeJS.org](https://nodejs.org) first

#### 💻 Installation and usage

Summary of the steps to be done:

```sh
git clone https://github.com/zaidmukaddam/ZeroChat zerochat
cd zerochat
npm install
cp .env.example .env 
// Change the .env variables if needed
npm run start
```

Explanation:

- Download the repo to your machine: **`git clone https://github.com/zaidmukaddam/ZeroChat zerochat`**
  - Enter the new directory with **`cd zerochat`**
- Install the dependencies for the project using **`npm install` or `yarn install`**
- Configure the environmental variables by renaming the `.env.example` file to `.env`, e.g. for defaults: **`cp .env.example .env`**
  - If you're using a Platform as a Service (PaaS), such as **AWS LightSail or Heroku**, configure it using the service's environment variables settings based of values in the `.env.example` file, and refrain from using the `.env` file
- Run the server using **`npm run start`**

## ⚠ Common Issues

### Nginx Issues

Proxying the requests through **Nginx** can be a bit problematic, since you have to turn `proxy_buffering off;` in your `location {...}` block.

Example:
```conf
server {
        server_name chat.example.com;
        location / {
                proxy_buffering off; # Fixes the issue!
                proxy_pass http://127.0.0.1:8000; # ZeroChat server running locally on port 8000
        }
        listen 80; # Nginx listening on port 80
}
```


## 📔 How it works

Here is the [article that explains how the chat is live without javascript](https://zaidmukaddam.biz/writing/stateful-http/)!

## Show your support

We love people\'s support in growing and improving. Be sure to leave a ⭐️ if you like the project and 
also be sure to contribute, if you're interested!
