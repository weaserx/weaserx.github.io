
# ADCS Installation Guide

## Installation

After successful installation and configuration of domain controller setup. we need to install the ADCS from `Add Roles and Feautures`

![Screenshot1](/ss/Pasted-image-20251028142327.png)

The installation wizard comes up after we clicked to the `Add Roles and Feautures`

![Screenshot2](/ss/Pasted-image-20251028142405.png)

we simply clicked next at the begin page.

![Screenshot3](/ss/Pasted-image-20251028142438.png)

at the `Installation Type` section we should chose the `Role-based` type 

![Screenshot4](/ss/Pasted-image-20251028142512.png)

at the `Server Selection` section we are choosing our DC.

![Screenshot5](/ss/Pasted-image-20251028142648.png)

at the `Server Roles` section we should check the ADCS box to install.

![Screenshot6](/ss/Pasted-image-20251028142716.png)

clicked `Add Features`

![Screenshot7](/ss/Pasted-image-20251028142952.png)

Then we need to chose role services. For now we can choose only the `Certificate Authority` to just install the CA and default templates. If we want to install other role services we can come back later to install.

![Screenshot8](/ss/Pasted-image-20251028143046.png)

And lastly we confirm our selections and clicked install.

![Screenshot9](/ss/Pasted-image-20251028143131.png)

## Configuration

After installation ends. At the top of the `Server Manager` we should have a notification. After the install we need to configure the ADCS like ADDS.

![Screenshot10](/ss/Pasted-image-20251028143632.png)

We clicked to `Configure Active Directory Certificate Services`

![Screenshot11](/ss/Pasted-image-20251028143703.png)

And the configuration wizard comes up. It asks for privileged user but automatically gets the our admin user.

![Screenshot12](/ss/Pasted-image-20251028143733.png)

We choose the CA for configure and clicked next

![Screenshot13](/ss/Pasted-image-20251028143807.png)

At `Setup Type` section its important to choose `Enterprise CA` if we are working in a domain.

![Screenshot14](/ss/Pasted-image-20251028143921.png)

Choosing the `Root CA` at `CA Type` section

![Screenshot15](/ss/Pasted-image-20251028144033.png)

If we are creating a new CA we can choose the `Create a new private key` option. This will create our root CA's private key to use forge operations.

![Screenshot16](/ss/Pasted-image-20251028144129.png)

`Cryptoghraphy` section can stay as default settings, after the install we can change it if we want.

![Screenshot17](/ss/Pasted-image-20251028144201.png)

`CA Name` section is defines the DN names and the CA Names for communation in the domain structure. we can set as default the CA Name or change if we want.

![Screenshot18](/ss/Pasted-image-20251028144243.png)

`Validity Period` section defines the life time of the generated certs. This setting by default comes with 5 years. What a persistence method to use :D. 

![Screenshot19](/ss/Pasted-image-20251028144322.png)

`Certificate Database` section defines the location of the databases. we can set it by default too.

![Screenshot20](/ss/Pasted-image-20251028144417.png)

At the `Confirmation` section we take a look to the settings and clicked to configure.

![Screenshot21](/ss/Pasted-image-20251028144544.png)

Configuring process started.

![Screenshot22](/ss/Pasted-image-20251028144645.png)

Configuring process succeeded.

## Check

After the setup process we can check the CA with any domain user.

```rb
certutil -dump
```
This command shows us the basic information about the ADCS.

![Screenshot23](/ss/Pasted-image-20251028144733.png)

We can check the ADCS with network joined linux too via `netexec`

```rb
netexec ldap 192.168.100.10 -u Administrator -p <pass> -M adcs
```
![Screenshot24](/ss/Pasted-image-20251028144840.png)

we can check for the templates with `certutil`
```rb
certutil -Template
```
![Screenshot25](/ss/Pasted-image-20251028145017.png)

As we can see we got `32` templates by default.
