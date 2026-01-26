# 🛠️ Setup Instructions

Complete guide to setting up your environment for the **AI Enabled Developer** course.

---

## 📋 Prerequisites

Before you begin, ensure you have:
- A computer running Windows, macOS, or Linux
- Stable internet connection
- Basic command-line knowledge
- Administrative privileges to install software

**Estimated Setup Time:** 30-45 minutes

---

## Step 1: Create GitHub Account

### New Users
1. Navigate to [github.com](https://github.com)
2. Click **Sign up** in the top-right corner
3. Enter your email address
4. Create a strong password
5. Choose a unique username
6. Complete the verification puzzle
7. Verify your email address via the link sent to your inbox

### Existing Users
If you already have a GitHub account, simply sign in at [github.com](https://github.com).

**✅ Verification:** You should be able to see your GitHub profile at `github.com/your-username`

---

## Step 2: Get GitHub Copilot Access

GitHub Copilot is available through several plans:

### For Students (FREE)
1. Visit [GitHub Student Developer Pack](https://education.github.com/)
2. Click **Get benefits**
3. Verify your student status with:
   - School-issued email address, OR
   - Student ID or proof of enrollment
4. Wait for verification (usually 1-2 days)
5. Once approved, GitHub Copilot is automatically included

### For Individuals
- **Monthly:** $10/month
- **Yearly:** $100/year (save $20)

**To Subscribe:**
1. Go to [GitHub Copilot Subscription](https://github.com/settings/copilot)
2. Click **Enable GitHub Copilot**
3. Choose your billing cycle
4. Enter payment information
5. Confirm subscription

### For Organizations
- **Business:** Contact GitHub Sales
- **Enterprise:** Contact GitHub Sales

**✅ Verification:** Visit [github.com/settings/copilot](https://github.com/settings/copilot) and confirm your subscription is active.

---

## Step 3: Install Visual Studio Code

### Windows
1. Visit [code.visualstudio.com](https://code.visualstudio.com/)
2. Click **Download for Windows**
3. Run the installer (`VSCodeUserSetup-{version}.exe`)
4. Accept the license agreement
5. Select installation location
6. **Important:** Check these options:
   - ✅ Add "Open with Code" action to Windows Explorer file context menu
   - ✅ Add "Open with Code" action to Windows Explorer directory context menu
   - ✅ Register Code as an editor for supported file types
   - ✅ Add to PATH
7. Click **Install**
8. Launch VS Code

### macOS
1. Visit [code.visualstudio.com](https://code.visualstudio.com/)
2. Click **Download for Mac**
3. Open the downloaded `.zip` file
4. Drag **Visual Studio Code** to the **Applications** folder
5. Launch VS Code from Applications

**Optional:** Add VS Code to your PATH:
- Open VS Code
- Press `Cmd+Shift+P`
- Type "shell command"
- Select **Shell Command: Install 'code' command in PATH**

### Linux

#### Debian/Ubuntu
```bash
sudo apt update
sudo apt install software-properties-common apt-transport-https wget
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
sudo apt update
sudo apt install code
```

#### Fedora/RHEL
```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
sudo dnf check-update
sudo dnf install code
```

#### Snap (Universal)
```bash
sudo snap install --classic code
```

**✅ Verification:** Open VS Code and you should see the Welcome screen.

---

## Step 4: Install GitHub Copilot Extensions

### Install GitHub Copilot
1. Open VS Code
2. Click the **Extensions** icon in the sidebar (or press `Ctrl+Shift+X` / `Cmd+Shift+X`)
3. In the search bar, type: **GitHub Copilot**
4. Find the extension published by **GitHub**
5. Click **Install**

### Install GitHub Copilot Chat
1. In the Extensions marketplace (same view)
2. Search for: **GitHub Copilot Chat**
3. Find the extension published by **GitHub**
4. Click **Install**

### Sign In to GitHub
1. After installing extensions, you'll see a notification to sign in
2. Click **Sign in to GitHub**
3. VS Code will open your browser
4. Authorize VS Code to access your GitHub account
5. You may be asked to authorize GitHub Copilot specifically
6. Return to VS Code

**Alternative Sign-In Method:**
- Press `Ctrl+Shift+P` / `Cmd+Shift+P`
- Type: **GitHub Copilot: Sign In**
- Follow the prompts

**✅ Verification:** 
- Look for the GitHub Copilot icon in the VS Code status bar (bottom right)
- It should show a checkmark or your account icon
- Open a new file and type a comment - you should see Copilot suggestions

---

## Step 5: Configure GitHub Copilot (Optional)

### Access Settings
1. Press `Ctrl+,` / `Cmd+,` to open Settings
2. Search for "copilot"

### Recommended Settings

**Enable/Disable for Specific Languages:**
```json
{
  "github.copilot.enable": {
    "*": true,
    "yaml": false,
    "plaintext": false,
    "markdown": false
  }
}
```

**Customize Suggestions:**
```json
{
  "github.copilot.advanced": {
    "inlineSuggestCount": 3
  }
}
```

**Keyboard Shortcuts:**
- Accept suggestion: `Tab`
- Dismiss suggestion: `Esc`
- Next suggestion: `Alt+]` / `Option+]`
- Previous suggestion: `Alt+[` / `Option+[`
- Trigger suggestion: `Alt+\` / `Option+\`

---

## Step 6: Install Git (If Not Already Installed)

### Check if Git is Installed
```bash
git --version
```

If you see a version number (e.g., `git version 2.39.0`), Git is already installed. Skip to Step 7.

### Windows
1. Download from [git-scm.com](https://git-scm.com/download/win)
2. Run the installer
3. Use default options (or customize as needed)
4. Restart your terminal/command prompt

### macOS
**Using Homebrew (recommended):**
```bash
brew install git
```

**Using Xcode Command Line Tools:**
```bash
xcode-select --install
```

### Linux
**Debian/Ubuntu:**
```bash
sudo apt update
sudo apt install git
```

**Fedora:**
```bash
sudo dnf install git
```

**✅ Verification:** Run `git --version` and confirm the output shows a version number.

---

## Step 7: Configure Git

Set your identity for Git commits:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

**Set Default Branch Name:**
```bash
git config --global init.defaultBranch main
```

**Optional:** Configure default editor
```bash
git config --global core.editor "code --wait"
```

**✅ Verification:** 
```bash
git config --list
```

You should see your name and email in the output.

---

## Step 8: Install Additional Tools (Optional but Recommended)

### Node.js (for JavaScript/TypeScript projects)
1. Visit [nodejs.org](https://nodejs.org/)
2. Download the LTS version
3. Run the installer
4. Verify: `node --version` and `npm --version`

### Python (for Python projects)
1. Visit [python.org](https://www.python.org/downloads/)
2. Download Python 3.11+ 
3. Run the installer
4. **Important:** Check "Add Python to PATH"
5. Verify: `python --version` or `python3 --version`

### Docker (for containerization)
1. Visit [docker.com](https://www.docker.com/products/docker-desktop/)
2. Download Docker Desktop for your OS
3. Install and launch
4. Verify: `docker --version`

---

## Step 9: Clone the Course Repository

### Using Command Line
```bash
# Navigate to your desired location
cd ~/Documents

# Clone the repository
git clone https://github.com/samipak458/AI-Enabled-Developer.git

# Navigate into the directory
cd AI-Enabled-Developer
```

### Using VS Code
1. Open VS Code
2. Press `Ctrl+Shift+P` / `Cmd+Shift+P`
3. Type: **Git: Clone**
4. Enter repository URL: `https://github.com/samipak458/AI-Enabled-Developer.git`
5. Choose a local folder
6. Click **Open** when prompted

**✅ Verification:** You should see the course files in your VS Code workspace.

---

## Step 10: Test Your Setup

### Test 1: GitHub Copilot Code Completion
1. Create a new file: `test.py`
2. Type the following comment:
   ```python
   # Function to calculate factorial of a number
   ```
3. Press `Enter` and wait a moment
4. You should see Copilot suggest a function implementation
5. Press `Tab` to accept

**✅ Expected Result:** Copilot suggests complete code.

### Test 2: GitHub Copilot Chat
1. Press `Ctrl+Alt+I` / `Cmd+Alt+I` to open Chat
2. Type: "Explain what a factorial function does"
3. Press `Enter`

**✅ Expected Result:** You receive a detailed explanation in the chat panel.

### Test 3: Git Integration
1. Create a new file in your repository
2. Save it
3. Open Source Control panel (left sidebar)
4. You should see your new file listed

**✅ Expected Result:** Git tracks your changes.

---

## 🎯 You're Ready!

Congratulations! Your development environment is now set up. 

### Next Steps:
1. ✅ **[Read the README](README.md)** - Understand the course structure
2. ✅ **[Start Module 1](modules/module1-intro-github-copilot/)** - Begin your learning journey
3. ✅ **[Join the Community](#)** - Connect with other learners

---

## ❓ Troubleshooting

### GitHub Copilot Not Working
- **Verify subscription:** Check [github.com/settings/copilot](https://github.com/settings/copilot)
- **Sign out and sign in:** Use Command Palette → "GitHub Copilot: Sign Out" then "Sign In"
- **Check extension status:** Look for errors in the Extensions panel
- **Restart VS Code:** Sometimes a simple restart fixes issues

### VS Code Won't Open
- **Windows:** Check if antivirus is blocking it
- **macOS:** Right-click VS Code → Open (if security blocks it)
- **Linux:** Check file permissions: `chmod +x /usr/bin/code`

### Git Commands Not Found
- **Restart terminal** after installation
- **Check PATH:** Ensure Git is in your system PATH
- **Reinstall Git** with "Add to PATH" option checked

### Extension Installation Fails
- **Check internet connection**
- **Disable firewall temporarily** during installation
- **Try manual installation:** Download `.vsix` file from [VS Code Marketplace](https://marketplace.visualstudio.com/)

---

## 📚 Additional Resources

### Official Documentation
- [VS Code Documentation](https://code.visualstudio.com/docs)
- [GitHub Copilot Docs](https://docs.github.com/en/copilot)
- [Git Documentation](https://git-scm.com/doc)

### Video Tutorials
- [VS Code Getting Started](https://code.visualstudio.com/docs/introvideos/basics)
- [GitHub Copilot Overview](https://www.youtube.com/watch?v=QZEf9E6PkqU)

### Support
- [VS Code Issues](https://github.com/microsoft/vscode/issues)
- [GitHub Community](https://github.com/orgs/community/discussions)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/github-copilot)

---

**Setup Guide Version:** 1.0  
**Last Updated:** January 2026

**Need Help?** Open an issue in the course repository or reach out to the community!

Happy Learning! 🚀
