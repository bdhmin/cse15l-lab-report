# Lab Report 3

**Bryan Min; A17153124**\
**February 11, 2022**

### Group Choice 1 - Streamline `ssh` Configuration

I created a custom nickname to the ieng6 server at ucsd. I made the nickname to be `cse15l`. When I went into `.ssh/`, I did not have a config file, so I created it using the command `vim config`.

I just used vim since it was just a couple lines to paste in, and I had to create the file anyways.

![Creating config file](https://user-images.githubusercontent.com/43192371/153670830-e2760791-6fd8-424f-a1f1-44f9d18e3b34.png)
![Adding lines to config file](https://user-images.githubusercontent.com/43192371/153670861-311dc379-15e2-40ad-b694-e06d0b766226.png)

Now when I run `ssh cse15l`, I can log in to the server—no need to memorize the username and hostname for the server.

![Logging in](https://user-images.githubusercontent.com/43192371/153670979-3bfad3a2-6902-4635-b2be-0b50d6c79d4f.png)

I decided to `scp` the file called `dummyfile` from my computer to the remote server. I simply ran `scp dummyfile cse15l` in the directory that contained the file.

![scp](https://user-images.githubusercontent.com/43192371/153672294-5e2e6013-4928-4310-8b3c-4fb14c765cdc.png)

In my ssh server, I found my file was copied over.

![server file found](https://user-images.githubusercontent.com/43192371/153672376-8a775a92-08eb-4e93-a44b-a1fe18d48600.png)
