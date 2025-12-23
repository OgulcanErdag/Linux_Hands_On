# Hands-on Linux-Plus-04 : Using Package Managers in Linux-Plus

​
Purpose of the this hands-on training is to teach the students how to use package managers in Linux-Plus.
​

## Learning Outcomes

​
At the end of the this hands-on training, students will be able to;
​

- Explain what is package management.
  ​
- Work with most common package management tools.
  ​
- Install, upgrade, configure and remove software packages using package management tools.
  ​

## Outline

​

- Part 1 - Using package managers ('yum' and 'apt')
  ​

## Part 1 - Using Package Managers ('yum' and 'apt')

​

- Update Amazon Linux-Plus Instance.
  ​

```bash
sudo yum update
```

- Update Ubuntu's package list. This command updates the local repo database but do not install any package.
  ​

```bash
sudo apt update
```

- Upgrade the packages. This command installs the listed available packages.

```bash
sudo apt upgrade
```

- Check if 'git' is installed on Amazon Linux-Plus instance or Amazon Linux-Plus 2023 instance.
  ​

```bash
git --version
```

- Check if 'git' is installed on Ubuntu instance.
  ​

```bash
git --version
```

- Install git on Amazon Linux-Plus instance.
  ​

```bash
sudo yum install git
```

- Uninstall git on Amazon Linux-Plus instance.
  ​

```bash
sudo yum remove git
```

- Install git on Amazon Linux-Plus instance without any interruption.
  ​

```bash
sudo yum install git -y
```

- Uninstall git on Amazon Linux-Plus instance without any interruption.
  ​

```bash
sudo yum remove git -y
```

- Check the version of git installed on Amazon Linux-Plus instance.(There should be no info, because it's just removed a minute ago)
  ​

```bash
git --version
```

- Explain why there is still version info.
- Install git on Amazon Linux-Plus instance without any interruption.
  ​

```bash
sudo yum install git -y
```

- Uninstall git with dependencies on Amazon Linux-Plus instance without any interruption.
  ​

```bash
sudo yum autoremove git -y
```

- Check the version of git installed on Amazon Linux-Plus instance.(There should ne no info, because it's just removed a minute ago)
  ​

```bash
git --version
```

- Uninstall git on Ubuntu instance.
  ​

```bash
sudo apt remove git
```

- Check the version of git installed on Ubuntu instance.(There should be no info, because it's just removed a minute ago)
  ​

```bash
git --version
```

- Install git on Ubuntu instance without any interruption.
  ​

```bash
sudo apt install git -y
```

- Uninstall git with dependencies on Ubuntu instance without any interruption.
  ​

```bash
sudo apt autoremove git -y
```

- Check the info for the git package installed on Amazon Linux-Plus instance.
  ​

```bash
sudo yum info git
```

- Check the info for the git package installed on Ubuntu instance.
  ​

```bash
sudo apt info git
```

- List all available packages for Amazon Linux-Plus instance.
  ​

```bash
sudo yum list
```

- List all available packages for Ubuntu instance.
  ​

```bash
sudo apt list
```

- List all available git packages for Amazon Linux-Plus instance.
  ​

```bash
sudo yum list git
```

- List all available git packages for Ubuntu instance.
  ​

```bash
sudo apt list git
```

- List all installed packages on Amazon Linux-Plus instance.
  ​

```bash
sudo yum list installed
```

- List all installed packages on Ubuntu instance.
  ​

```bash
sudo apt list --installed
```

- List all available versions of git packages on Amazon Linux-Plus instance.
  ​

```bash
sudo yum --showduplicates list git
```

- List all available versions of git packages on Ubuntu.

```bash
sudo apt-cache madison git
```

- Check the version of git installed on Amazon Linux-Plus and Ubuntu instance.
  ​

```bash
git --version
```

- Uninstall git with dependencies on Amazon Linux-Plus instance without any interruption.
  ​

```bash
sudo yum autoremove git -y
```

- Uninstall git with dependencies on Ubuntu without any interruption.
  ​

```bash
sudo apt-get remove git -y
```

- Install a previous version of git on Amazon Linux-Plus instance.
  ​

```bash
sudo yum --showduplicates list git
sudo yum install git-2.14.5-1.amzn2 -y
```

- Install a previous version of git on Ubuntu instance.
  ​

```bash
sudo apt-cache madison git
sudo apt install git=1:2.43.0-1ubuntu7 -y --allow-downgrades
```

- Check the version of git installed on Amazon Linux-Plus instance.
  ​

```bash
git --version
```

- Update git and check the version.
  ​

```bash
sudo yum update git -y
git --version
```

- All commands for Amazon Linux-Plus 2023 Instance.
  ​

```bash
sudo dnf update
sudo dnf upgrade
git --version
sudo dnf install git
sudo dnf remove git
sudo dnf install git -y
sudo dnf remove git -y
sudo dnf install git -y
sudo dnf autoremove git -y
sudo dnf info git
sudo dnf list
sudo dnf list git
sudo dnf list installed
sudo dnf --showduplicates list git
git --version
sudo dnf autoremove git -y
sudo dnf --showduplicates list git
sudo dnf install git-2.14.5-1.amzn2 -y
git --version
sudo dnf --showduplicates list git
sudo dnf list git
sudo dnf update git -y
git --version
```

- DNF Command in Linux-Plus with Practical Examples :

```bash
https://tecadmin.net/dnf-command-in-Linux-Plus/
```

- Comparing Amazon Linux-Plus 2 and Amazon Linux-Plus 2023

```bash
https://docs.aws.amazon.com/Linux-Plus/al2023/ug/compare-with-al2.html#package-manager
```
