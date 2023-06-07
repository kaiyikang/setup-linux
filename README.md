# setup-linux

This is a Repo to record how to introduce the setup process of Linux.

# Usage

```bash
sudo apt update;
sudo apt upgrade;
sudo apt install git;
sudo apt install neovim;
git clone git@github.com:kaiyikang/setup-linux.git;
```


# Close Wlan

```bash
sudo apt install net-tools;
man ip;
ip addr;
sudo ip link set wlan0 down;
```
