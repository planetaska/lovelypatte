---
layout: post
author: aska

---
Multiple GitHub accounts on the same computer

[https://stackoverflow.com/questions/3860112/multiple-github-accounts-on-the-same-computer](https://stackoverflow.com/questions/3860112/multiple-github-accounts-on-the-same-computer "https://stackoverflow.com/questions/3860112/multiple-github-accounts-on-the-same-computer")

**Relevant steps from the first link:**

1. Generate an SSH-key:

       ssh-keygen -t ed25519 -C "john@doe.example.com"
       

   Follow the prompts and decide a name, e.g. `id_ed25519_example_company`.
2. Copy the SSH public-key to GitHub from `~/.ssh/id_ed25519_doe_company.pub` and tell ssh about the key:

       ssh-add ~/.ssh/id_ed25519_doe_company
       
3. Create a `config` file in `~/.ssh` with the following contents:

       Host github-doe-company
         HostName github.com
         User git
         IdentityFile ~/.ssh/id_ed25519_doe_company
       
4. Add your remote:

       git remote add origin git@github-doe-company:username/repo.git
       

   or change using:

       git remote set-url origin git@github-doe-company:username/repo.git
       

***

Also, if you're working with multiple repositories using different personas, you need to make sure that your individual repositories have the user settings overridden accordingly:

Setting user name, email and GitHub token – Overriding settings for individual repos[https://help.github.com/articles/setting-your-commit-email-address-in-git/](https://help.github.com/articles/setting-your-commit-email-address-in-git/ "https://help.github.com/articles/setting-your-commit-email-address-in-git/")

Hope this helps.

**Note:** Some of you may require different emails to be used for different repositories, from git **2.13** you can set the email on a directory basis by editing the global config file found at: `~/.gitconfig` using conditionals like so:

    [user]
        name = Default Name
        email = defaultemail@example.com
    
    [includeIf "gitdir:~/work/"]
        path = ~/work/.gitconfig
    

And then your work-specific config `~/work/.gitconfig` would look like this:

    [user]
        name = Pavan Kataria
        email = pavan.kataria@example.com
    

Thank you @alexg for informing me of this in the comments.