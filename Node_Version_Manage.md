# Install Node with /node version manager
Installing Node.js with a version manager is a great way to manage multiple Node.js versions on your system. The two most popular version managers for Node.js are nvm (Node Version Manager) and fnm (Fast Node Manager). Here's how to install and use nvm to manage Node.js versions.

**Step 1: Download and install `nvm`** :
    
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
    
**Step 2: Restart your terminal or reload your shell configuration** :
    
    source ~/.bashrc   # or ~/.zshrc, depending on your shell
    
**Step 3: Verify the installation** :

    nvm ls-remote

**Step 3: Check available Node.js versions** :

    nvm --version

**Step 3: Install a specific version** :

    nvm install <version>

**Step 3: Check the installed Node.js version** :

    node --version



