# Instructions on how to set up and use github through the command line for the first time.
- Assumes you have just created a new repository online
- Here is how to push a new .ipynb file to that repository.

1. Make sure `git` is installed.\
   `module spider git`
2. Configure your account.\
   `git config --global user.name "USERNAME"`\
   `git config --global user.email "EMAIL@DOMAIN.COM"`
3. Clone the repository
   - change directory to the directory into which you want to place the repository that you are going to clone\
     `cd /path/to/your/directory `
   - then clone the repo\
     `git clone https://github.com/username/repository.git`
