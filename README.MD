## xray_docker_reality


## Basic Usage
If you don't have docker installed, please install docker first

```
curl -fsSL get.docker.com -o get-docker.sh && sh get-docker.sh
```

If you have already installed docker, you can directly use the following command. After running,
the image will be downloaded automatically and the container will be started.
EXTERNAL_PORT is the port you want to use. As shown below, you will use port 443

clone git
```
git clone https://github.com/koopichi/rlty.git && cd rlty
```
build container
```
docker build -t reality .
```

```
EXTERNAL_PORT=443
docker run -d --name arash --restart=always -p $EXTERNAL_PORT:443 -e EXTERNAL_PORT=$EXTERNAL_PORT reality
```

Check the log to get the configuration information, as shown below, just follow the prompts to configure the client,

```
docker logs -f xray_reality 
```

## Advanced usage

If you don't want to use port 443, you can customize the port, for example, use port 8443, as shown below

```
EXTERNAL_PORT=8443
docker run -d --name xray_reality --restart=always -p $EXTERNAL_PORT:443 -e EXTERNAL_PORT=$EXTERNAL_PORT reality
```

If you want to start multiple reality services, you can use different container names, and be careful not to conflict with the ports.
As shown below, you will start two reality services, using ports 444 and 445 respectively

```
EXTERNAL_PORT=444
docker run -d --name xray_reality_1 --restart=always -p $EXTERNAL_PORT:443 -e EXTERNAL_PORT=$EXTERNAL_PORT reality
EXTERNAL_PORT=445
docker run -d --name xray_reality_2 --restart=always -p $EXTERNAL_PORT:443 -e EXTERNAL_PORT=$EXTERNAL_PORT reality
```

If you don't want to use the default parameters, you can customize the parameters, such as using a custom UUID,
as well as custom target address and server name, as shown below. For supported custom parameters, please refer to the environment variable description below

Use spaces to separate multiple SERVERNAMES, for example: www.apple.com images.apple.com

Please note that if you use custom parameters, you need to ensure the correctness of the parameters yourself, otherwise the container may fail to start
```
EXTERNAL_PORT=443
docker run -d --name xray_reality --restart=always -p $EXTERNAL_PORT:443 -e EXTERNAL_PORT=$EXTERNAL_PORT -e SERVERNAMES="www.digicert.com" -e DEST="www.digicert.com:443"  reality
```

Use the following command to delete the created container, as shown below, you need to replace xray_reality with your own container name (the name set by --name)

```
docker rm -f xray_reality
```


## environment variable
You can set the following environment variables to customize XRay's configuration.
* UUID: XRay's unique user identifier. If not set, the script will automatically generate a random UUID.
* DEST: Destination address. The default is www.apple.com:443.
* SERVERNAMES: A list of server names. The default is www.apple.com images.apple.com.
* PRIVATEKEY: private key. If not set, the script will automatically generate a new private key and corresponding public key.
* NETWORK: Network type. The default is tcp.

## constant
* flow：xtls-rprx-vision
* security：reality
* shortIds：leave blank
