<img align="right" src="img/beame.png">
_The Beame SDK allows you to establish a HTTPS session between machines without public IPs. This SDK  allows you to create credentials and use them to identify machines. It’s a simple way to use encryption-based identity in web and mobile applications. This transparent security infrastructure can be used in any network, global or local, to create credentials, bind them to users’ hardware, and get strong, crypto-based authentication. This mitigates risk for services that host credentials to require users to prove identity._
_Beame-SDK employs hierarchical structure. The most top level is the Layer-0 (L0) - network root. L1 considered child of L0. L0 may have any number of children (L1s), each of those can have its own "children" L2's and so on. Any lower level "child" can be tracked, by cryptography, up to its L0 parent. This is the base for building proprietary chain of trust._ 
[Click to Get Started Now!](https://registration.beameio.net/)

## Common Uses for Beame SDK Network Infrastructure

See the example folder to copy-paste and try it for yourself!

 - Build your own networking application
 - Define chain of trust for devices in your Beame-SDK based network
 - Multi-factor authentication
 - Check signatures of arbitrary data
 - Encrypt arbitrary data so that only a specified entity can decrypt it
 - Decrypt arbitrary data that was sent to one of the entities you own (encrypted with one of your public keys)
 - Sign arbitrary data with any of your certificates
 - Global, local, or hybrid socket.io chat over TLS
 - Patient ID in clinics using mobile phone
 - BYOD in local networks (access behind NAT)

### By deploying your network using Beame infrastructure, you can:

1. Quickly host a public HTTPS server on a local machine (does not require public static IP, DMZ, nor port forwarding);
2. Generate credentials and assign your own meaning to them (identity);
3. Deploy services that are accessible from the Internet or only from your LAN without network reconfiguration.

## Here's how:
1. You will get a unique hostname under the Beame subdomain;
2. You will generate your private key locally;
3. You will get a matching certificate from Beame (signed by a root CA).

### Table of Contents
 - [System Requirements](#system-requirements)
 - [Installation Guide](#installation-guide)
 - [Quick Start](#quick-start)
 - [Getting Started - Mac](#mac-system-requirements)
 - [Getting Started - Windows](#windows-system-requirements)
 - [High Level Architecture](#high-level-architecture)
 - [Beame Network Infrastructure](#beame-network-infrastructure)
 - [Custom Provisioning Workflow](#custom-provisioning-workflow)
 - [Custom Client Provisioning Flow Chart](#custom-client-provisioning-flow-chart)
 - [Beame CLI (credentials, running test server, encryption)](#beame-cli)
 - [Beame NodeJS API](#beame-nodejs-api)
 - [Examples of full-stack of credentials and https server with express support](#sample-https-server)

:heavy_exclamation_mark: **Note: for the documentation that matches the latest NPM, please see the [`prod` branch](https://github.com/beameio/beame-sdk/tree/prod).**
 
## System Requirements
Mac OS or Windows 8.1 (or higher);
NPM installed on your machine;
for Mac: See the Mac instructions if current shell version does not support auto-completion.

## Installation Guide
_If you already know how Beame-SDK is working and want to skip the intro, [jump directly to start!](#beame-cli)_
### Beame-SDK proposes a number of options to start:
1. Create your own L0
_You will create three tiers of credentials (each with multiple components: a RSA key pair, a hostname under Beame.io's domain, and a matching publicly trusted x509 certificate)._

    1.1. First, generate [Developer credentials.](https://registration.beameio.net/)
    1.2. Second, generate application credentials. We call this level an Atom.
    1.3. Create your Client server credentials.  We call this level an Edge-Client.

Our extended demo ([see it here](#running-test-server)) has two features - chat, or file server:
 - To access the chat, just copy the URL to your browser. (By the way, you can freely send it to other people on other networks. The server is global and the TLS is real).
 - To access the file share function, open the `url/shared`.

## Quick Start

### Light Configuration *coming soon 
1. Install the Beame SDK by running `npm install -g beame-sdk` and this will quickly output a URL that will be a hostname for your first HTTPS Server with your new Beame Credentials. 

### Full Configuration: 

1. Register as a developer, by submitting your email at [https://registration.beameio.net/](#https://registration.beameio.net/) 
2. Install the Beame SDK by running `npm install -g beame-sdk`
3. Copy the unique activation command from the email you receive, it should look like: `beame creds createDeveloper --developerFqdn ndfxfyerylk6uvra.v1.beameio.net --uid 1d138bfc-4a37-48e7-a60d-0190037fda5f`
4. Start your first HTTPS server by running `beame servers startFirstBeameNode`. It should print to your console something that looks like `Server started on https://fdddr5ggsyzhk6m8.v1.r.p.edge.eu-central-1b-1.v1.p.beameio.net this is a publicly accessible address`

You now have your public HTTPS server running. Just copy-paste the address to any web browser.

## Mac System Requirements
First ensure that your bash version is 4.3 or higher (`echo $BASH_VERSION`). If not - upgrade it.
Take care to replace 4.3.46 from snippets below by your new bash version:
```
brew update && brew install bash
Add new shell to available shells:
sudo bash -c 'echo /usr/local/Cellar/bash/4.3.46/bin/bash >> /etc/shells'
```
Change to the new shell:
`chsh -s /usr/local/Cellar/bash/4.3.46/bin/bash`

Open new terminal and run:
```
brew tap homebrew/versions
brew rm bash-completion
brew install bash-completion2
```
Add following instructions to your .bashrc file (if you don't have .bash_profile in your Home directory, create one :)
```
if [ -f $(brew --prefix)/share/bash-completion/bash_completion ]; then
    . $(brew --prefix)/share/bash-completion/bash_completion
fi

source /usr/local/lib/node_modules/beame-sdk/src/cli/completion.sh
```
Open new terminal and begin using beame-sdk cli with auto-completion.

## Windows System Requirements

Before running `npm install -g beame-sdk` please make sure you have OpenSSL installed in `C:\OpenSSL-Win64` . If you you already have OpenSSL installed at that location, skip the instructions below and just issue `npm install -g beame-sdk`. If you don't have OpenSSL in `C:\OpenSSL-Win64`, one of the possible ways of installing OpenSSL is described below (Install Visual C++ Build Tools and Python 2.7, Upgrade NPM, Install Perl, Install OpenSSL). The procedure was tested on Microsoft Windows Server 2012 R2 Standard and Windows 10. We recommend to use your “Windows PowerShell” and run it with administrator rights for the following commands:

### Install Visual C++ Build Tools and Python 2.7

`npm install --global --production windows-build-tools`. This typically takes 5 to 10 minutes, depending on the internet connection.

### Upgrade NPM

`npm -g install npm@latest`

### Install Perl

Perl is needed for building OpenSSL. If you already have Perl installed, please skip the `Install Perl` section.

Get Perl from
`https://downloads.activestate.com/ActivePerl/releases/5.24.0.2400/ActivePerl-5.24.0.2400-MSWin32-x64-300558.exe` (SHA256 is `9e6ab2bb1335372cab06ef311cbaa18fe97c96f9dd3d5c8413bc864446489b92`)
or another source.
 This version of Perl [might have](https://community.activestate.com/node/19784) [security](https://www.virustotal.com/en/file/9e6ab2bb1335372cab06ef311cbaa18fe97c96f9dd3d5c8413bc864446489b92/analysis/) [issue](https://www.metadefender.com/#!/results/file/c869301df9424b02aa49ce15d7bce692/regular/analysis) but my estimation is that it's false positive. Consider installing other versions or Perl built by other companies.

### Install OpenSSL

Download and extract `https://www.openssl.org/source/openssl-1.0.1t.tar.gz` (other versions might work but were not tested)

Using "Visual C++ 2015 x64 Native Build Tools Command Prompt" under `C:\Program Files (x86)\Microsoft Visual C++ Build Tools\` in the OpenSSL directory issue the following commands:

    perl Configure VC-WIN64A no-asm --prefix=C:\OpenSSL-Win64
    .\ms\do_win64a.bat
	# If the following "clean" fails it's OK, just continue with following commands
    nmake -f ms\ntdll.mak clean
    nmake -f ms\ntdll.mak
    nmake -f ms\ntdll.mak install

	npm install -g beame-sdk

#Beame.io Networking Solution Overview

## High Level Architecture

![high level architecture](img/SDKbuildingBlocks.jpg)

All routable nodes created with the Beame SDK are clients of Beame services. From the application perspective, they are HTTPS servers.

### Elements of the High Level Architecture
 - *Local Client* - hosts that are created with local IP
 - *Edge Client* - hosts that are accessible from the Internet, clients of *Edge Servers*
 - *Clients* - actual end users (mobile devices)
 - *Customers* - owners of networks created with Beame Infrastructure (described below)
 - *Developer* - holder of credentials to directly request Beame provision services
 - *Atom* - application under *developer*, used as a master node for networks built with Beame Infrastructure

## Beame Network Infrastructure

Actions to employ:
 - *Developer* registration using [email-based procedure](https://registration.beameio.net/)
 - Deployment of *Atom* as entity to control access permissions for all devices intended to be a part of the network (customers and clients)
 - Deployment of *Customer Edge Clients*. Each of the hosts, created on this step, shall be used as a Customer’s provisioning entry point. Any *client* that needs to be allowed into the network must undergo registration procedure as described below
 - Provisioning *clients* into *Customer*’s network

## Custom Provisioning Workflow

![provisioning workflow](img/ProvisioningClient.jpg)

*CMPS* (Customer Managed Provisioning Server) credentials are pinned in the *Atom*, during *CMPS* deployment, prior to the first run of the service.

The custom provisioning process requires *Customer* to deploy *Edge Clients* (*CMPS*s) with corresponding permissions under Customer's internal security policy.

The custom provisioning process uses the *Atom* as single authorization point.

## Custom Client Provisioning Flow Chart

![provisioning flowchart](img/clientProvisionFlowchart.jpg)

### There are three interleaved flows in the provisioning process:
 - *CMPS flow* - process takes place on the *Customer* provisioning station, controls the whole process;
 - *Atom flow* - background process controlled by Customer’s *Atom*;
 - *Client flow* - process that takes place on the mobile device. Requires corresponding mobile Beame SDK services.

# Mastering the Beame-SDK

## Beame CLI

If you have completed the ["Quick Start"](#quick-start) above, and know how your future application will look, you can feel free to use all of what's described below.
At any moment, using beame-sdk, you can see all credentials you currently own by running:
 - `beame creds show`

### CLI - credentials

The following commands are used for acquiring and manipulating certificates.

* `beame creds list [--type {developer|atom|edgeclient}] [--fqdn fqdn] [--format {text|json}]` - list certificates
* `beame creds show [--type {developer|atom|edgeclient}] [--fqdn fqdn] [--format {text|json}]` - show certificate details
* `beame creds createAtom --developerFqdn developerFqdn --atomName atomName [--format {text|json}]` - create *atom* entity under current *developer*
* `beame creds createEdgeClient --atomFqdn atomFqdn [--format {text|json}]` - create *edge client* entity under the given *atom*
* `beame creds createLocalClient --atomFqdn atomFqdn [--count count] --edgeClientFqdn edgeClientFqdn [--format {text|json}]` - create *local client* entity under the given atom paired to existing *edge client*
* `beame creds renew [--type {developer|atom|edgeclient}] [--fqdn fqdn]`
* `beame creds purge [--type {developer|atom|edgeclient}] [--fqdn fqdn]`

### Running test server

* `beame servers launchHelloWorldServer --edgeClientFqdn edgeClientFqdn` - run a "Hello World" HTTPS server for the specified hostname
* `beame.js servers launchFirstChat [--sharedFolder sharedFolder]` - run chat example for first hostname in creds list
* `beame.js servers launchChat --edgeClientFqdn edgeClientFqdn [--sharedFolder sharedFolder]` - run chat example for the specified hostname

### Beame.io CLI - encryption

* `beame crypto encrypt [--data data] [--fqdn fqdn]` - encrypts the given data so that only the owner of the specified entity can decrypt it
* `beame crypto decrypt [--fqdn fqdn] [--data data]` - decrypts the given data. You must be the owner of the given entity
* `beame crypto sign [--data data] [--fqdn fqdn]` - signs the given data as the specified entity
* `beame crypto _checkSignature [--fqdn fqdn] [--data data] --signature signature` - verifies the correctness of the signature

## Beame NodeJS API
[Extended JsDoc generated documentation - here](https://beameio.github.io/beame-sdk/index.html)

_The idea behind the Node.js SDK APIs is that you can employ Beame CLI functionality in your own Node.js project._

Receive publicly trusted cert with a pseudo-random routable hostname and run your new TLS(SSL) server in the same flow (or later, whenever you see it fit).

Current SDK release intends extensive CLI usage (see description above). So Node.js APIs provide a high level of access.

Be aware that API on each level requires credentials created on the previous/higher level:

To use any API from beame-sdk include
`var beameSDK = require ("beame-sdk");`

### Atom level commands
Requires developer credentials (developer fqdn/hostname) + atomName (your application name)
To create new atom under current developer:
```
    beameSDK.creds.createAtom(devHostname, atomName, amount, function(data){//amount - number of atoms to create
        //atom level hostname returned in: <data.hostname>
    });
 ```
### Edge Client level commands
Requires atom credentials (atom fqdn/hostname). atomHostName - app level hostname created in previous step
To create new edgeClient under current atom:
```
   beameSDK.creds.createEdgeClient(atomHostname, amount, function(data){//amount - number of edgeClient to create
        //edge level hostname returned in: <data.hostname>
    });
```

## Sample HTTPS Server
Beame-sdk provides sample https server, that allows Beame client to build and run fully a functional https server with express support and with credentials created in steps described above

Export environment variable 'BEAME_PROJ_YOURPROJECTNAME' with value of edge-client-hostname (edgeClientFqdn)
In your server main.js create your server with following command:
```
    	var BeameServer = beameSDK.BaseHttpsServer.SampleBeameServer(host, PROJECT_NAME, appExpress,
        function (data, app) {
            //your code
        });
```
### Input parameters:
*`host` - edge hostName (pass <null> if you use environment variable - see below)
*`PROJECT_NAME` - name of environment variable that contains edgeClient hostname (pass <null> if you provided full hostname in first parameter)
*`appExpress` - express object. If you don't need express in your application, pass <null>
*`function(data,app){}` - callback, returned app - created http object

## Copy-paste examples

## Steps to take before you run below code:

1. Create web page with your preferred software (like Keynote -> export HTML on Mac).
2. Store your new web page in `public` folder in directory of your future web server.
3. Run `npm init` in project directory (*enter* to all options that *npm* asks)
4. In same location install `npm install beame-sdk --save`
5. Install *express* package by `npm install express --save`
6. Create index.js and copy-paste into it code below.
```
"use strict";
var beameSDK = require ("beame-sdk");
var express = require('express');
var devHostname = "put-here-Hostname-you-got-when-creating-developer";
var appName = "MyBeameTestServer";
var appExpress = express();
var edgeHostname;
appExpress.use(express.static(__dirname + '/public'));

var runTestBeameServer = function(){
    beameSDK.BaseHttpsServer.SampleBeameServer(edgeHostname, null, appExpress, function (data, app) {
        console.log('Server started on: https://'+edgeHostname);
        appExpress.get('/', function(req, res) {
            res.sendFile(path.join(__dirname + '/index.html'));
        });
            // process http events here with <app> if needed
    });
};

beameSDK.creds.createAtom(devHostname,appName, 1, function(data){
	console.log('Just created atom with host:'+data.hostname);
	beameSDK.creds.createEdgeClient(data.hostname, 1, function(edgeData){
		edgeHostname = edgeData.hostname;
		console.log('Congrats! My new hostname is: '+ edgeHostname);
		setTimeout(runTestBeameServer, 2000);//JIC - wait dns to update
	});
});
```
7. Run it with `node index.js`
8. In console output you will see something like:
`Server started on: https://h3a6ipg1jz95x35n.v1.r.p.edge.eu-central-1b-1.v1.p.beameio.net`
`{ Hostname: 'h3a6ipg1jz95x35n.v1.r.p.edge.eu-central-1b-1.v1.p.beameio.net' }`

9. Go to web brower and direct it to your new secure web server by copying https://*hostname* from console output
That's it. You have your own https server running on your local machine, accessible from anywhere in the world :)

### Sample HTTPS server - short

Below code snippet is actually a part of the larger code above. So it requires all needed installations (npm/express/beame-sdk/placing-html-files-in-*public*-folder) to be performed prior to run.
In order to see credentials that you have created, use `beame creds list` in terminal. *Hostname*, that is listed in row named *edgeclient* ,is the one, that you'll need to provide to *SampleBeameServer* as *hostname*.

```
"use strict";
var beameSDK = require ("beame-sdk");
var express = require('express');
var appExpress = express();
var hostname = "h3a6ipg1jz95x35n.v1.r.p.edge.eu-central-1b-1.v1.p.beameio.net";
appExpress.use(express.static(__dirname + '/public'));

var runTestBeameServer = function(){
    beameSDK.BaseHttpsServer.SampleBeameServer(hostname, null, appExpress, function (data, app) {
        console.log('Server started on: https://'+hostname);
    });
};
runTestBeameServer();
```
