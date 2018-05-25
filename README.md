# How to control your rig by SSH from all over the world ?

### Disclaimer

I'm not responsible for anything.I wouldn't recommand this tutorial to someone without any computer science knowledge. Doing this tutorial not correctly can lead to some intrusion in your network.

## Get started
This tutorial will explain you how to control your mining rig from all over the world by using SSH.

## Prerequisites:
- Any kind of router
- A server on the same local network than your mining farm (Raspberry, Home Server ..)
- As much rig as you want

## Step I - Dynamic DNS & Domain name

> Some ISP provide a static IP, if you have one you can skip this step and move forward to the step II.

Alright. The first thing that you need in order to control your rig remotely is a static IP. If you are not using a static IP you'll need to know the public IP of your rig, and it can change at anytime (depends on ISP). Moreover, if you are in Mexico and you want to access your rig which is based in New York, how are you suppose to know its public IP.

If your ISP do not provide you a static IP, we will use a dynamic DNS. Indeed, it's not a static IP address but it's an address (like "http://whaterver.io") which is supposed to always point to the object with a dynamic IP that it has been connected to (here our router).

We are then going to use [no-ip](https://www.noip.com) which will allow us to have a dynamic DNS and therefore an address pointing indefinitly to our router :

- Create an account
- Register an hostname

Once this is done, go to your router configuration page, it should be [192.168.1.1](192.168.1.1) and search for something about "Dynamic DNS". Usually they should ask you about your login and password (that you setted 3 lines above).

To make sure that everything is working just type on google the hostname you created. For instance, if you created the hostname "helloworld.ddns.me" then just type it on google address search bar. If everything worked, you should be able to see the EXACT same thing on helloworld.ddns.me and 192.168.1.1.

Ok now that we did that we can access to our router from everywhere in the world, using the address of our dynamic DNS.

## Step II - Configure local static IP address for your server and your rigs

We need now to give to all of our electronic device (server and mining rigs only tho) a local static IP address.

- With DLink: [Configure local static IP address with DLink router](http://blog.dlink.com/mastering-static-ip-addresses-2/)

## Step III - Port configuration

In order to connect to our server by SSH (which use natively the port 22) we need to tell someone that if it request access to the port 22 he will be directly redirected to the server. To do so we need to do a port forwarding and forward the port 22 of our box to our server. Like this, if someone try to access to the port 22 of our box, he will be redirect to the server on the port 22.

I won't explain you here how to port forward. There is plenty of tutorial out there. Just write on google : $(theNameOfYourRouter) + "port forward tutorial".

## Step III - Connect to it

So now, we should have:
- a dynamic DNS which redirecting to our router
- a local static IP address for our server and each mining rigs
- our router's port 22 forwarded to our server's port 22

If all of that is done, then you are all set up !

If it's a raspberry then the command to connect to your server should be :

``` ssh pi@hellworld.ddns.me ```

The default ssh password of a raspberry Pi is "raspberry" but change it rigth now !

Now that you have access to your home server by SSH, you can then access to your mining rigs by connecting to them with SSH again, ssh inside shh .. (SSHception). Remember that we set static local IP address for all of our mining rig, so we know the local IP of each rig, and most importantly, it won't change !

To do, open the SSH config file (on the server, not on your computer) :

``` nano ~/.ssh/config ```

And add whatever host you wanna connect to (here our mining rigs) :

```
Host rig1
    HostName 192.168.1.10
    User ethos
```

Now, you can access to your rigs by simply doing :

``` ssh rig1 ```

And you are all set up !
