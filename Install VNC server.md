# Install VNC server `x11vnc`

## Step 1:  Install VNC server

1. Open terminal in TX2(Ctl + Atl + T)
    ```
    sudo apt-get install x11vnc -y
    ```

2. Set password x11vnc
    ```
    x11vnc -storepasswd
    ```
    Terminal show the same bellow:

    ```
    Enter VNC password:
    ```
    Set you password VNC

    ```
    Verify password:
    ```
    Retype VNC password

    ```
    Write password to /home/morvan/.vnc/passwd?  [y]/n
    ```
    Type 'Y'

    Finally type two line

    ```
    sudo x11vnc -storepasswd [your_password] /etc/x11vnc.pass
    ```
    
    **Start server**
    ```
    x11vnc -forever
    ```
## Step 2: Check ip TX2
1. Check ip of Jetson TX2
    ```
    ifconfig
    ```
## Step 3: In you computer. Install [VNC viewer](https://www.realvnc.com/en/connect/download/viewer/) and enjoy it
.

***

**Note: If you want to Convince **apt-get** \*not\* to use IPv6 method.**
Add `-o Acquire::ForceIPv4=true` when running `apt-get`.

If you want to make the setting persistent just create */etc/apt/apt.conf.d/99force-ipv4* and put *Acquire::ForceIPv4 "true"*; in it:
```
echo 'Acquire::ForceIPv4 "true";' | sudo tee /etc/apt/apt.conf.d/99force-ipv4
```