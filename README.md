<div align="center">

 <h1> PoC quic vulnerability 🌐</h1>

<em>This project demostrates how a Denial-of-Service (DoS) attack can be caused by a flaw in the <code>aioquic</code> QUIC implementation. By taking advantage of how CRYPTO frames are handled, a malevolent client can cause unmanaged memory allocation and ultimately bring down the server.</em>

<img src="Attack Diagram.png" alt="Attack Diagram" border="0" width="80%">

</div>

<br><br>
<div align="left">

<h1>⚙️ How To Use</h1>

- [Set up Environment 💻](#set-up-environment-)
- [Run the Exploit 👾](#run-the-exploit-)

</div>

## Set up Environment 💻

To reproduce the vulnerability, use **two separate virtual machines** (based on [Ubuntu 22.04](https://releases.ubuntu.com/22.04/)) with:

- [Git](https://git-scm.com)
- [Python 3.10+](https://www.python.org/downloads/)
- [pip](https://pip.pypa.io/en/stable/installation/)

One VM will act as the **server**, the other as the **attacker client**.

```bash
# Clone the repository
$ git clone https://github.com/pintorem/Network-sec.git
$ cd Network-sec

# (Optional) Create a conda environment
$ conda create -n quic-vuln python=3.10 -y
$ conda activate quic-vuln

# Install dependencies
$ pip install -r requirements.txt
```


## Run the Exploit 👾

Once the environment is ready on both virtual machines, follow these steps:

### 🖥️ On VM1 (Server)

```bash
# Start the vulnerable aioquic server
$ python3 examples/http3_server.py --certificate tests/ssl_cert.pem --private-key tests/ssl_key.pem
```

### 🖥️ On VM2 (Client)

```bash
# Start the aioquic client attacker
$ python3 examples/http3_client.py
```
