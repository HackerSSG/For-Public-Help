Here’s the updated version:


# **Git Commands Guide for Uploading a Project**

## **Step-by-Step Workflow**

### **1. Navigate to Your Project Folder**
Open the terminal or command prompt and navigate to your project directory:
```bash
cd C:\Users\ENGR MUHAMMAD USMAN\Desktop\SC LABS\LAB-10-GIT-TEST\test-repo\coffee-shop
```

---

### **2. Initialize a Git Repository**
To start tracking your project with Git:
```bash
git init
```

---

### **3. Check the Remote Repository**
Verify if a remote repository is already set up:
```bash
git remote -v
```

---

### **4. Add or Update a Remote Repository**
If the remote does not exist, add one:
```bash
git remote add origin https://github.com/hackerssg/test-repo.git
```

If the remote already exists and needs updating:
```bash
git remote set-url origin https://github.com/hackerssg/test-repo.git
```

---

### **5. Add Files to Staging**
To add all files in your project directory to the staging area:
```bash
git add .
```

---

### **6. Commit Changes**
Save your changes with a descriptive message:
```bash
git commit -m "Initial commit: Added Coffee Shop application"
```

---

### **7. Pull Changes from the Remote Repository**
If the remote repository has changes you don’t have locally, pull them first:
```bash
git pull origin master --allow-unrelated-histories
```

---

### **8. Push Changes to the Remote Repository**
Push your local changes to GitHub:
```bash
git push -u origin master
```

---

### **9. Check the Status of Your Repository**
To see which files are staged, unstaged, or untracked:
```bash
git status
```

---

## **Extra Commands**

### **Check Current Branch**
To see the branch you're working on:
```bash
git branch
```

---

### **Create and Switch to a New Branch**
Create a new branch and switch to it:
```bash
git checkout -b <branch-name>
```

---

### **Push a New Branch to Remote**
Push the new branch to the remote repository:
```bash
git push -u origin <branch-name>
```

---

### **Force Push (If Necessary)**
If you encounter errors while pushing, use force push:
```bash
git push origin master --force
```

---

That's your guide in proper Markdown format! Let me know if you'd like to add more commands or details. 🚀
````
