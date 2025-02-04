# Creating a test- repo:

- We are going to authenticate the access to github using SSH rather than HTTPS like before. 

Step 1:

1-Generate SSH key pair on your local machine:
```bash
 $ ssh-keygen -t rsa -b 4096 -c "maramalhmaidi@gmail.com"
 ```
2- name your key: maram-gt-key
- two keys are created:
    - maram-gt-key
    - maram-gt-key.pub

step 2: Register the public key on Github:
- from settings on github go to ssh keys 
- add new key
- on local machine run this code:
```bash
cat maram-gt-key.pub
```

![alt text](<Screenshot 2025-02-04 155137.png>)

step 3: Register private key on the local machine. Run the following code:

- The following code would start an ssh agent and provides proccess ID.
```bash
eval `ssh-agent -s`
```
- Add the private key
```bash 
ssh-add maram-gt-key
```
- Authenticate local machine ssh connection to github:
```bash
ssh -T git@github.com
```

step 4:create a new repo on github:
- name : tech501-ssh
- make it public


5- Push changes made to github:
- cd to your github repo and mkdir "tech501-ssh"
- cd to the tech501-ssh dir
- initialize repo; git init
- create a README.md file with one line message; $ echo "#tech501-test-ssh" > README.md
- git branch -M main
- git remote add origin git@github.com:marmari9/tech501-ssh-.git
- git add .
- git commit -m"message"
- git push -u origin main


![alt text](<Screenshot 2025-02-04 160839.png>)
