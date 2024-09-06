# 1. Configure of frps serving for trilium in LAN

## 1.1 Specify following variables in `.env` file for your domain.

```bash
# nginx-proxy environments

# The port your App listen on.
VIRTUAL_PORT: w8080

# The (sub)domain of your application.
VIRTUAL_HOST: "sub.domain.com"


## frps listen port, if you use another one, you must make "bind_port" as the same in frps.ini .
FRPS_BIND_PORT=7003

## Deploy root path, default is current directory.
INSTALL_ROOT_PATH=/opt/servers

## Directory for deployment at INSTALL_ROOT_PATH
SERVER_NAME=frps_trilium_ray

## Directory name for configuration file of frps, default is cfgs at current directory.
CFGS_DIR='cfgs'



# Selfsigned certificates parameters for `1_init.sh`

## Server domain for CA, here is same as FRPS_SERVER_DOMAIN for selfsigned certificates.
CA_SERVER_DOMAIN='domain.com'

## Server domain for frps deployment.
FRPS_SERVER_DOMAIN='domain.com'

## Server ip for frps deployment.
FRPS_SERVER_IP='192.168.0.1'
```


## 1.2 Specify following variables in `cfgs/frps.toml` file for your domain.
Just refer to official document.
The most required variables are:

* `bindPort` : Listening port for frpc connection.
* `vhostHTTPPort` : The port which frpc required to expose.

* `auth.token` : token for authentication between frpc and frps.
* `subDomainHost` : subdomain for frps routing.


# 2. Initialize services environment

Run the following script to generate selfsigned certificates for frps and frpc.

```bash
./1_init.sh
```

# 3. Launch:

```bash
docker compose up -d
```

