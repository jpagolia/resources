# Instructions on how to set up and use git and GitHub through the command line for the first time.
- Assumes you have just created a new repository online
- Here is how to push a new .ipynb file to that repository.
- Here is a great resource: https://happygitwithr.com/install-intro#install-intro
- Another great resource: https://github.com/bhattlab/scg_tools

1. Make sure `git` is installed.
   ```
   module spider git
   ```
2. Configure your account.
   ```
   git config --global user.name "USERNAME"
   git config --global user.email "EMAIL@DOMAIN.COM"
   ```
3. Set up ssh key
   - Check to see if you have any ssh keys already set up:
     ```
     ls ~/.ssh/*.pub
     ```
   - If you don't see id_ed25519.pub, then you likely need to create a key. Create new public-private key pairing by doing this:
     ```
     ssh-keygen -t ed25519 -C "your_email@stanford.edu"
     ```
     You will see this output:
     ```
     Generating public/private ed25519 key pair.
     Enter file in which to save the key (/home/username/.ssh/id_ed25519): # just press Enter to use the default filename
     Enter passphrase (empty for no passphrase): # recommended to enter a passphrase
     Enter same passphrase again: # enter it again
     Your identification has been saved in /home/jpagolia/.ssh/id_ed25519.
     Your public key has been saved in /home/username/.ssh/id_ed25519.pub.
     The key fingerprint is:
     The key's randomart image is:
     ```
4. Start the ssh-agent and add your new key:
   ```
   eval "$(ssh-agent -s)"; ssh-add ~/.ssh/id_ed25519
   ```
5. Add the public key to GitHub:
   ```
   cat ~/.ssh/id_ed25519.pub
   ```
   Copy the entire output line and add it to your personal GitHub profile on the website in GitHub → Settings → SSH and GPG keys → New SSH key.
   
6. Test SSH
   ```
   ssh -T git@github.com
   ```
   You should see:
   ```
   Hi USERNAME! You've successfully authenticated, but GitHub does not provide shell access.
   ```
7. Clone the repository
   - Change directory to the directory into which you want to place the repository that you are going to clone
      ```
      cd /PATH/TO/YOUR/DIRECTORY
      ```
   - Then clone the repo using ssh to connect to github
     ```
     git clone git@github.com:ORGANIZATION/REPOSITORY.git
     ```
8. Add the new notebook to the repository
    - change directory to the repository that you just cloned
     ```
     cd RESPOSITORY
     ```
    - add the new notebook file to the repository. Copy it to the repository directory first with `cp /PATH/TO/NOTEBOOK.ipynb NOTEBOOK.ipynb`.
     ```
     git add NOTEBOOK.ipynb # make sure you've gone into the jupyter notebook and cleared all the output so it doesn't take an age and a half to commit
     ```
9. Commit it to the repository. This saves your changes to the local repository but does not change the remote (online) repository at all.
    ```
    git commit -m "Add notebook" # include a "message" about what this commit is doing
    ```
10. Check that status of your local repository versus the remote repository to make sure someone else hasn't committed to the remote repository while you were working.
    ```
    git status
    ```
    You can also inspect divergence using
    ```
    git fetch; git log --oneline --decorate --graph --all
    ```
11. Push your changes from your local repository to your remote repository
    ```
    git push origin main
    ```
     
