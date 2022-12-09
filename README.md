# Localization Testing at Scale
Test your applications globally and at scale. By combining Sauce Labs and WonderProxy, you not only get the great benefits of globalized testing delivered by WonderProxy but also the scalability and robustness of testing on the Sauce Labs platform.

## Prerequistes
- A Sauce Labs account ([Log in](https://accounts.saucelabs.com/am/XUI/#login/) or sign up for a [free trial license](https://saucelabs.com/sign-up)).
- Your Sauce Labs [Username](https://app.saucelabs.com/user-settings).
- A working development environment for one of the supported Selenium languages: Java, C#, Python, or Ruby.
- [Sauce Connect](https://docs.saucelabs.com/secure-connections/sauce-connect/installation/#downloading-sauce-connect-proxy)
- A WonderProxy account ([Log in](https://wonderproxy.com/login))

## Getting Started

### WonderProxy – Getting Set Up

To get started, **ensure you have**:

1.  Added your desired servers to your [WonderProxy account](https://wonderproxy.com/my/servers).
2.  Located your WonderProxy [username](https://wonderproxy.com/my/settings).
3.  Generated a WonderProxy [proxy token](https://wonderproxy.com/my/settings#proxy-tokens). You'll enter this proxy token whenever the proxy configuration asks for a password.
4.  Determined the [hostname](https://wonderproxy.com/my/servers) of the server you wish to connect to (e.g. `newyork.wonderproxy.com`).

>ℹ️   A username and proxy token are required to log into the proxy servers. Users cannot use Single Sign-On for proxy server authentication.

#### Server Ports

WonderProxy's port numbering scheme allows you to select whether additional proxy headers are included. Ports with the same last two digits will use the same exit IP. The available ports are listed below:

|Port|Description|
|----|------------|
|10000|Full proxy headers are added to each request. **X-Forwarded-For** is sent to the server and **X-Host-IP** is returned to the client.|
|11000|No headers are added to the request sent **to the destination server**; the response includes an **X-Host-IP** header, providing the IP of the server that handled the request.|
|12000|No headers are added in **either** direction.|


> ℹ️    Requests that are transmitted via HTTPS are not modified by the proxy in any manner. The traffic remains encrypted as it passes through the proxy and no headers are ever added.

### Sauce Labs – Getting Set Up

1.  [Download the Sauce Connect Proxy client](https://docs.saucelabs.com/secure-connections/sauce-connect/installation/#downloading-sauce-connect-proxy) on your machine.
>⛔️   ALWAYS USE THE LATEST VERSION
>
>Using older Sauce Connect versions may impact your ability to launch a tunnel or cause other technical issues.    
2.  Extract the .zip file and move the folder to your machine's [home directory](https://en.wikipedia.org/wiki/Home_directory).
3.  Open your terminal and navigate to the Sauce Connect Proxy client bin directory.

## Starting Your Tunnel

Once you have completed all of the steps above, you are now ready to start your first localized tunnel on Sauce Labs.

> ℹ️   In this example, we will be using the London proxy server on WonderProxy. For different locations substitute the below snippet with the appropriate `tunnel-name`, `proxy`, and `logfile`.

1. Paste the snippet below into your terminal and run it. This will launch the tunnel.
``` bash
./sc -u $SAUCE_USERNAME -k $SAUCE_ACCESS_KEY --region us-west --tunnel-name london_tunnel --proxy "london.wonderproxy.com:11000" -w "$WONDERPROXY_USER:$WONDERPROXY_TOKEN" --logfile london.log
```
2. To confirm your tunnel is up, look for the confirmation message in your terminal:
```bash
Secure remote tunnel provisioned. Tunnel ID: 876620c18...

Sauce Connect is up, you may start your tests.
```

## Using Your New 'Global' Tunnel
Follow the instructions found [here](https://docs.saucelabs.com/secure-connections/sauce-connect/setup-configuration/basic-setup/#basic-setup-with-a-test-script) to learn how to hook your tunnel into your automated test scripts.

If you would like to test manually, you can find instructions [here](https://docs.saucelabs.com/secure-connections/sauce-connect/quickstart/#run-test) on how to proceed. However, in the URL field that is mentioned, `http://localhost:3000` may not be what you want to test but instead something like `https://www.etsy.com` to see how the site now loads for traffic in London.






