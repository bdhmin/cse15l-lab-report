# CSE 15L Lab Report 1 Week 2

**Bryan Min; A17153124**\
**January, 15, 2022**

### 1. Installing VScode

- I navigated to [this link](https://code.visualstudio.com/) and click "Download ...".
- Once I downloaded, followed the steps the installer displayed.
- Once fully installed, I open VScode:

<img width="1397" alt="vscode" src="https://user-images.githubusercontent.com/43192371/149246304-ed28582b-e7e9-43b7-bb06-7420c35526cd.png">

### 2. Remotely Connecting

- I opened terminal and typed in `ssh cs15lwi22---@ieng6.ucsd.edu` and replaced the '---' with my user account character combination I accessed on https://sdacs.ucsd.edu/~icc/index.php.
- When prompted for a password, I typed in my password.
- Then I was logged in to the remote server:

<img width="757" alt="Screen Shot 2022-01-12 at 5 03 22 PM" src="https://user-images.githubusercontent.com/43192371/149247314-7310f9ca-d71b-48b6-9267-bef717ba483b.png">

### 3. Trying Some Commands

- `ls` lists all files and directories in current directory I am in.
- `pwd` displays the current filepath I am in.

<img width="335" alt="Screen Shot 2022-01-12 at 5 07 44 PM" src="https://user-images.githubusercontent.com/43192371/149247709-78920ced-4cd1-4b6f-99db-9e0261a82291.png">

### 4. Moving Files with `scp`

- Calling `scp <filename> cs15lwi22---@ieng6.ucsd.edu:~/` copied the file I included in <filename> into my remote server
- This prompted me to enter my password which I did.
  
<img width="385" alt="Screen Shot 2022-01-12 at 11 21 57 PM" src="https://user-images.githubusercontent.com/43192371/149284017-eed6588d-cf2b-45c9-9372-65dce1394da2.png">

### 5. Setting an SSH Key
  
- Called `ssh-keygen` on my client
- Generated the key in recommended location with no passphrase.

*Already generated SSH key*\
<img width="551" alt="Screen Shot 2022-01-12 at 11 26 15 PM" src="https://user-images.githubusercontent.com/43192371/149284603-2e0b6323-db90-40ed-9f82-0691c6b78662.png">

### 6. Optimizing Remote Running  

- In ssh server, `mkdir .ssh`
- In client, `scp /Users/<username>/.ssh/id_rsa.pub cs15lwi22---@ieng6.ucsd.edu:~/.ssh/authorized_keys`
- Then the next time I log into remote server, I will not have to type in my password.
  
<img width="717" alt="Screen Shot 2022-01-12 at 11 34 38 PM" src="https://user-images.githubusercontent.com/43192371/149285710-0bb0ca90-e788-44ff-9e6f-261666a53ead.png">

  

  
