# 🛠️ Linux Environment Debugging Process

## 1. Understand the Problem
- Clarify what is not working: **service**, **script**, **network**, **filesystem**, or **performance**.
- Gather details: **error messages**, **logs**, **recent changes**, and **expected behavior**.

---

## 2. Check System Health

```bash
uptime            # Check load average
free -h           # Check memory usage
df -h             # Check disk usage
top / htop        # Real-time CPU and memory monitoring
```

## 3. Logs Are Your Best Friend

```bash
dmesg             # Kernel ring buffer (hardware/driver issues)
journalctl        # Systemd logs
journalctl -xe    # Critical logs and errors
/var/log/syslog   # General logs (Debian/Ubuntu)
/var/log/messages # General logs (RHEL/CentOS)
```
## 4. Debugging Services (Systemd)

```bash
systemctl status <service>     # Check service status
journalctl -u <service>        # View logs for a specific service
systemctl restart <service>    # Restart the service
```

## 5. Check Processes & Resource Usage

```bash
ps aux | grep <name>           # Search for running processes
top                            # Monitor system resource usage
htop                           # Enhanced version of top
strace -p <pid>                # Trace system calls of a running process
```

## 6. File & Permission Issues

```bash
ls -l                          # List permissions
stat <file>                    # Detailed file metadata
chmod 755 <file>               # Change permissions
chown user:group <file>        # Change ownership
```

## 7. Network Issues

```bash
ping <host>                    # Test network connectivity
traceroute <host>              # Trace route to destination
netstat -tuln                  # List open ports
ss -tuln                       # Modern replacement for netstat
curl -v http://localhost:8000  # Test web service
```

## 8. Script or Application Errors

**Run scripts with debugging flags:**

```bash
bash -x script.sh              # Bash script with trace
python -m pdb script.py        # Python debugger
node --inspect script.js       # Node.js debugger
Redirect output to a file:
./script.sh > output.log 2>&1
```

## 9. Check Environment Variables

```bash
env            # Print all environment variables
echo $VAR_NAME # Print the value of a specific variable
```

## 10. Package or Dependency Issues

```bash
which <command>         # Locate the full path of a command
ldd <binary>            # Check shared library dependencies of a binary
dpkg -l | grep <pkg>    # Check installed packages (Debian/Ubuntu)
rpm -qa | grep <pkg>    # Check installed packages (RHEL/CentOS)
```
