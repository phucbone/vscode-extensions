# ssh

```sh
# SSH Port Forwarding
ssh -i /path/to/your-key.pem \
  -L <local-port>:<database-private-ip>:<database-port> \
  <username>@<bastion-host-public-ip>

# -i /path/to/your-key.pem: chỉ định file private key của bạn.
# -L <local-port>:<database-private-ip>:<database-port>: tạo tunnel chuyển tiếp từ cổng local trên máy bạn tới database trong private subnet.
# <username>: user trên bastion-host (ví dụ ec2-user).
# <bastion-host-public-ip>: IP public của bastion-host.

# SSH ProxyJump
ssh -i /path/to/your-key.pem \
  -J <username>@<bastion-host-public-ip> \
  <username>@<database-private-ip>

# -J: Connect to the target host by first making an ssh connection to the jump host described by destination and then establishing a TCP forwarding to the ultimate destination from there.
# Multiple jump hops may be specified separated by comma characters.
# IPv6 addresses can be specified by enclosing the address in square brackets.
# This is a shortcut to specify a ProxyJump configuration directive.
# Note that configuration directives supplied on the command-line generally apply to the destination host and not any specified jump hosts.
# Use ~/.ssh/config to specify configuration for jump hosts.
```

```config
# ~/.ssh/config
Host bastion
    HostName <bastion-host-public-ip>
    User ec2-user
    IdentityFile /path/to/your-key.pem

Host database
    HostName <database-private-ip>
    User ec2-user
    IdentityFile /path/to/your-key.pem
    ProxyJump bastion
```
