# BESI-C Post Deployment Intructions

## Watches

## Relays 

### Data Offloading

#### Terminology 
**Terminal/Shell** [Terminal/Shell](https://en.wikipedia.org/wiki/Shell_(computing))
>  In computing, a shell is a computer program which exposes an operating system's services to a human user or other programs. In general, operating system shells use either a command-line interface (CLI) or graphical user interface (GUI), depending on a computer's role and particular operation. It is named a shell because it is the outermost layer around the operating system.\[[1](https://en.wikipedia.org/wiki/Shell_(computing))\]

**SSH** - [Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell)
>  The Secure Shell Protocol (SSH) is a cryptographic network protocol for operating network services securely over an unsecured network. Its most notable applications are remote login and command-line execution.  
>  SSH applications are based on a client–server architecture, connecting an SSH client instance with an SSH server. SSH operates as a layered protocol suite comprising three principal hierarchical components: the transport layer provides server authentication, confidentiality, and integrity; the user authentication protocol validates the user to the server; and the connection protocol multiplexes the encrypted tunnel into multiple logical communication channels. \[[2](https://en.wikipedia.org/wiki/Secure_Shell)\]
#### Programs
`ls` - [List Directory Contents](https://linux.die.net/man/1/ls)
- Purpose:
    - List the contents of a directory
- Usage:
    - `ls [OPTION]... [FILE]...`
- Example:
    - List contents of current directory
    - `ls`
    - List contents of /home/pi
    - `ls /home/pi`
    - List contents of current directory including hidden/.dirs
    - `ls -a`

`cp` - [Copy Files and Directories](https://linux.die.net/man/1/cp)
- Purpose:
    - Copy file(s)/dir(s) to another dir
- Usage:
    - `>`
- Example:
    - >

`mv` - [Move (Rename) Files](https://linux.die.net/man/1/mv)
- Purpose:
    - Move file(s)/dir(s) or rename a file/dir
- Usage:
    - `>`
- Example:
    - >

`rm` - [remove files or directories](https://linux.die.net/man/1/rm)
- Purpose:
    - >
- Usage:
    - `>`
- Example:
    - >

`ssh` - [Open SSH Client](https://linux.die.net/man/1/ssh)

- Purpose:
    - Remotely controlling another device via the Terminal
- Usage:
    - `ssh [-1246AaCfgKkMNnqsTtVvXxYy] [user@]hostname [command]`
- Example:
    - Connect to relayXXXX 
    - `ssh pi@besic-relay-XXXX`  
    - Connecto to relay at IP 192.168.17.DDD
    - `ssh pi@192.168.17.DDD`

`scp` - [Secure Copy](https://linux.die.net/man/1/scp)

- Purpose:
    - Moving files between two devices
- Usage:
    - `scp [-1246BCpqrv] [-c cipher] [-F ssh_config] [-i identity_file] [-l limit] [-o ssh_option] [-P port] [-S program] [[user@]host1:]file1 [[user@]host2:]file2`
- Example:
    - Copy file named data.csv on relayXXXX to current directory
    - `scp pi@besic-relay-XXXX data.csv .`

#### Process
How to remove/offload data from the Relays:

1. Connect to **BESI-Network** WiFi
1. Open Terminal / Command Prompt
1. Connect to BaseStation over SSH
    - `ssh pi@<basestation hostname/ip>` *Note: BaseStation IP Address is 192.168.17.1 by default*
    - `[password]`
1. View Connected Devices
    - `arp -a`
1. Connect to Relays over SSH
    - `ssh pi@<relay hostname/ip>`
    - `[password]`
1. Check the sources
    - `ls /var/besic/data`
    - `ls /var/besic/archive`
1. Exit Device(s)
    - `exit`
1. Offload data backups
    - `scp pi@<relay hostname/ip>:/var/besic/archive/* .`
    - `[password]`
1. Delete Data Backups
    - SSH Back into device
        - `ssh pi@<relay hostname/ip>`
        - `[password]` 
    - `sudo rm -rf /var/besic/archive/*`
1. Exit Relay
    - `exit`
1. Run magical upload script 
    - `MAGIC`
1. Since right now the magical upload script doesn't really exist... copy data to your own machine and upload the data. Manually
