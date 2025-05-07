![](/images/shellprompt.png)
- ~ means home directory (/home/harsh)

# Understanding the Folder Structure

### Explanation of System Directories

### **Symbolic Links (Less Significant)**
| Directory | Description |
|-----------|-------------|
| `/sbin -> /usr/sbin` | System administration binaries, typically for root user; symlinked to `/usr/sbin` for unified management. |
| `/bin -> /usr/bin` | Essential command binaries for all users (e.g., `ls`, `cp`); now symlinked to `/usr/bin` for consistency. |
| `/lib -> /usr/lib` | Core shared libraries needed by binaries in `/bin` and `/sbin`; symlinked to `/usr/lib`. |

![](/images/usr.png)

### **Important System Directories**
| Directory | Description |
|-----------|-------------|
| `/boot` | Contains bootloader files (like GRUB) and Linux kernel; critical for system startup. |
| `/usr` | Main directory for user programs, libraries, documentation, and system-wide resources. |
| `/var` | Variable data: logs, mail, print spool, and files that grow over time. |
| `/etc` | System-wide configuration files and scripts; most settings for installed software live here. |

### **User & Application-Specific Directories**
| Directory | Description |
|-----------|-------------|
| `/home` | Personal directories for each user; stores user files, settings, and data. |
| `/opt` | Optional or third-party software packages; often used for large, self-contained apps. |
| `/srv` | Data for services provided by the system (e.g., web, FTP); rarely used in containers. |
| `/root` | Home directory for the root (admin) user; separate from regular user homes for security. |

### **Temporary & Volatile Directories**
| Directory | Description |
|-----------|-------------|
| `/tmp` | Temporary files for all users and applications; cleared on reboot. |
| `/run` | Volatile runtime data (e.g., process IDs, sockets); exists only while system is running. |
| `/proc` | Virtual filesystem exposing kernel and process information as files; dynamic and read-only. |
| `/sys` | Virtual filesystem for kernel, device, and hardware info; used for system tuning and monitoring. |
| `/dev` | Device files representing hardware (disks, terminals, etc.) and virtual devices. |

### **Mount Points**
| Directory | Description |
|-----------|-------------|
| `/mnt` | Standard location for temporarily mounting filesystems (e.g., external drives). |
| `/media` | Auto-mount point for removable media (USB drives, CDs, SD cards). |
| `/data` | Custom mount point, often used for persistent or shared data (e.g., Windows volume in WSL). |

- Any user that you create the home directory it starts with `/home/Ubuntu` ` /home/harsh`
- For root is `/root`
