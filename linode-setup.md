### Signup on VPS Hosting Provider

- https://www.linode.com/ (The One I'll Be using) | $100 Free Credit Available)
- https://www.digitalocean.com/ (For Long Term people) | $100 Free Credit Available)
- https://www.vultr.com/ (For Millennials)  | $50 Free Credit Available)
- https://galaxygate.net/ (Best Hands down for the price)

Will soon provide affiliate links for all above ^ mentioned. helps both you and me  🤷😉 

### Setting up VPS

Once you're done with Signup, Confirm Email Verification
and then Login to your hosting provider and follow the steps below.

>Should be very similar for all providers, 
Just have to choose root and some distribution of linux.. after that its 99% same.


#### Click on Create Linode
![](https://i.imgur.com/YDSOQhB.png)

#### Choose Distribution and Region

- I recommend going for ubuntu as its very well documented and LTS version makes it stable
- Choose a region based on where you live, or what is your target audience

![](https://i.imgur.com/L4LOtxl.png)
#### Choose a Plan
![](https://i.imgur.com/ex0WGnY.png)
#####  I Recommend Going for a Dedicated 4GB at the moment considering you have 100$ free credit 
if not, Linode 4GB in Shared should be good too.

#### Choose a label, just a name 🙋‍♂️
##### Choose a strong Root Pass, at first this is the only thing to make sure your server is secure
similar to : 
>t;Uz"6bWiWiu=h\ads%$#moadasd#$#@$

![](https://i.imgur.com/iK2Y1j9.png)
#### SSH Keys, Vlan, Backup will talk about these in a future thread
![](https://i.imgur.com/7C0GHb3.png)

- Don't forget to Turn on Private IP ~

#### Reconsider the price
and move forwared with the purchase
![](https://i.imgur.com/5YABpwL.png)
#### Click Create Linode.

___________________________
### Accessing the VPS
![](https://i.imgur.com/8X8Ta11.png)

#### Download and install Putty : https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html
![](https://i.imgur.com/NFAeiYt.png)
##### Type in the Server IP Address and Click Open and click on Accept below.
![](https://i.imgur.com/03jlr1o.png)

### Login Credentials
##### By Default you will have username : root and password that you set while setting up server
![](https://i.imgur.com/E36KIeV.png)
Once you are in, you will see root@localhost:~#
so here, root is the user
and localhost is the hostname
~ says you are in root directory
| # says you have root/admin permissions

#### Set the Hostname

A hostname is used to identify your Linode using an easy-to-remember name. Your Linode’s hostname doesn’t necessarily associate with websites or email services hosted on the system, but see our guide on using the hosts file if you want to assign your Linode a fully qualified domain name.

Your hostname should be something unique, and should not be www or anything too generic. Some people name their servers after planets, philosophers, or animals. After you’ve made the change below, you may need to log out and log back in again to see the terminal prompt change from localhost to your new hostname. The command hostname should also show it correctly.

- hostnamectl set-hostname example-hostname | Change hostname.. don't want that localhost 😅

>hostnamectl set-hostname cyberalliance

After doing that reboot server from Control panel of your hosting.
You should then see, this post boot
![](https://i.imgur.com/yqmxSPn.png)

#### Check for system/package updates and install all of them

> apt update && apt upgrade -y

once its all done you will see,
![](https://i.imgur.com/uLIW4AO.png)
**DONE**



### Now your Basic Linode VPS Setup is done.

