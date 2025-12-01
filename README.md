# Ubuntu Hostname Change Guide

This document provides a **clear, structured, and professional** guide explaining how to change the hostname on Ubuntu. It is written for developers, system administrators, or anyone maintaining Linux systems.

---

## Introduction

A **hostname** is the unique identifier assigned to a machine on a network. It appears in the terminal prompt, plays a role in local and remote communication, and is used by several system services. Keeping the hostname consistent and meaningful is good practice for system organization and maintenance.

This guide describes two methods for changing the hostname on Ubuntu:

* the **recommended method** using `hostnamectl`
* the **manual method** using configuration files

---

## Method 1 — Recommended: Using `hostnamectl`

Ubuntu systems that use **systemd** provide the `hostnamectl` tool, which is the safest and most consistent way to modify the hostname.

### **1. Check the current hostname**

Use the following command to inspect the active hostname and related system information:

```bash
hostnamectl
```

### **2. Set the new hostname**

Replace `NEW_HOSTNAME` with the desired hostname:

```bash
sudo hostnamectl set-hostname NEW_HOSTNAME
```

This updates the static, pretty, and transient hostnames automatically.

### **3. Update `/etc/hosts`**

To ensure proper local name resolution, manually update the hosts file:

```bash
sudo nano /etc/hosts
```

Look for a line similar to:

```
127.0.1.1    current-hostname
```

Replace it with:

```
127.0.1.1    NEW_HOSTNAME
```

Save the file and exit:

* **CTRL + O** → ENTER
* **CTRL + X**

### **4. Reboot the system**

A reboot ensures all services load the new hostname:

```bash
sudo reboot
```

---

## Method 2 — Manual Editing (Alternative)

This method directly edits configuration files. It works, but requires more caution.

### **1. Modify `/etc/hostname`**

```bash
sudo nano /etc/hostname
```

Replace the existing hostname with the new one.

### **2. Update `/etc/hosts`** (same as in Method 1)

```bash
sudo nano /etc/hosts
```

Update the `127.0.1.1` entry to reflect the new hostname.

### **3. Reboot**

```bash
sudo reboot
```

---

## Notes and Best Practices

* Hostnames should contain only **lowercase letters, digits, and hyphens**.
* Avoid spaces or special characters.
* Always update `/etc/hosts` to prevent name resolution issues.
* Most system services will automatically pick up the new hostname after reboot.

---

## Verify the Change

After the system restarts, verify the hostname:

```bash
hostnamectl
```

```bash
hostname
```

Both commands should return the updated hostname.

---

## Additional Recommendations

* Choose meaningful hostnames when working with multiple servers or virtual machines (e.g., `data-node01`, `workstation-ubuntu`, `analysis-server`).
* If the machine participates in a domain or uses services like SSH, consider verifying the configuration after the change.

---

## Conclusion

Changing the hostname on Ubuntu is straightforward when using `hostnamectl`. Updating both `hostname` and `/etc/hosts` ensures smooth system behavior and proper resolution. This guide provides a reliable procedure suitable for production environments, educational material, and documentation within a GitHub repository.
