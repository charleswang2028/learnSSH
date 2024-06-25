# test github ssh key 
charleswong2028@gmail.com

[How to Set Up Multiple SSH Keys for GitHub Accounts on macOS?](https://pratapsharma.io/github-miltiple-key)

Floppy Diskette
Pratap Sharma
About
Blogs
Courses
Dark Mode
Checkout the latest course: Building REST APIs with Flask and Python in 2023


How to Set Up Multiple SSH Keys for GitHub Accounts on macOS?
Article Author
Pratap Sharma
November 26th, 2023- 1770 views /4 mins read
github-accountmultiple-github-accountgitgithub
Upon joining my new company, I encountered the requirement of maintaining a separate GitHub account for work-related repositories. This posed a challenge as I needed to manage both my personal and work GitHub accounts on a single machine. To address this, I undertook a step-by-step approach to set up multiple GitHub accounts on my Mac, ensuring a seamless workflow for both.

Step 1: Generate SSH Keys
Open your terminal and generate SSH keys for both accounts:

ssh-keygen
ssh-keygen -C work@domain.com
These commands create public/private key pairs located in the ~/.ssh directory:

~/.ssh/id_rsa
~/.ssh/id_rsa.pub
~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub
Once the keys are generated run this command:

eval "$(ssh-agent -s)"
The above command is used to start the SSH agent and set up the necessary environment variables.

Step 2: Modify SSH Config File
Create or modify the ~/.ssh/config file:

vim ~/.ssh/config
Add the following configuration:

# GitHub for personal
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa

# GitHub for work
Host github.com-work
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519

Host *
   AddKeysToAgent yes
   IdentitiesOnly yes
Save the file.

Step 3: Add Keys to macOS Keychain
Run the following commands to add keys to the Keychain:

eval "$(ssh-agent -s)"
ssh-add -D # This will delete all identities previously added
ssh-add --apple-use-keychain ~/.ssh/id_rsa
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
Verify the added keys with:

ssh-add -l
Step 4: Add Public Keys to GitHub Accounts
Add the public keys to your GitHub accounts following GitHub's documentation.

Step 5: Test the Connection
Test the connection for both accounts:

ssh -T git@github.com
ssh -T git@github.com-work
You should see a successful authentication message.

Step 6: Clone the Repository
Clone repositories using the appropriate remote URLs:

For personal account:

git clone git@github.com/project.git
For work account:

git clone git@github.com-work:company/project.git
Step 7: Test it Out
Create a repository on GitHub, clone it, and configure user email and name for the local repository:

For work account:

git config --local user.email "work@domain.com"
git config --local user.name "work"
Now, you can seamlessly push and pull from GitHub repositories with multiple accounts.

We can follow the same tutorial for other vcs systems.

Learn More
A practical guide to data collection with OpenTelemetry, Prometheus and Grafana
Beginner's Guide to HTTP Methods and Status Codes
Flask and SQLAlchemy: Better Data Management
Please let me know if there's anything else I can add or if there's any way to improve the post. Also, leave a comment if you have any feedback or suggestions.






Discussions

Up next
Displaying Lakhs and Crores in Google Sheets: A Step-by-Step Guide
Best Practices for Naming REST API Endpoints
Pratap Sharma
Author
Hey, I’m Pratap, a full stack software engineer and an instructor. I write about what I know to help viewers like you. If you enjoy my content, please consider supporting what I do!

Coffee iconBuy me a coffee
PatreonBecome a Patron
Ko-fi
Patreon
Tweets
RSS
Newsletter
SIP Calculator
GitHub
GitHub
Youtube
Copyright © 2024. Pratap Sharma
