---
title: Setting Up a Virtual Private Network (VPN) for Secure Communication
description: 
published: true
date: 2023-02-04T22:55:36.603Z
tags: 
editor: markdown
dateCreated: 2023-02-04T22:55:31.251Z
---

- [Configuración de una red privada virtual (VPN) para una comunicación segura***Spanish** document is available*](/es/Knowledge-base/Backend/setting-up-a-virtual-private-network-vpn-for-secure-communication)
{.links-list}
- [为安全通信设置虚拟专用网络 (VPN)***Chinese Simplified** document is available*](/zh/Knowledge-base/Backend/setting-up-a-virtual-private-network-vpn-for-secure-communication)
{.links-list}
- [보안 통신을 위한 가상 사설망(VPN) 설정***Korean** document is available*](/ko/Knowledge-base/Backend/setting-up-a-virtual-private-network-vpn-for-secure-communication)
{.links-list}


# Setting Up a Virtual Private Network (VPN) for Secure Communication

A Virtual Private Network (VPN) allows you to create a secure connection to another network over the Internet. VPNs can be used to access region-restricted websites, shield your browsing activity from prying eyes on public Wi-Fi, and more.

Most Internet users don't need to worry about VPNs. If you're just trying to watch Netflix or encrypt your browsing data, you can use a free VPN service like TunnelBear. But if you're looking for more security or want to set up a VPN on your own server, you'll need to use a VPN server.

## What is a VPN Server?

A VPN server is a computer or virtual machine that acts as a gateway between your device and the Internet. When you connect to a VPN server, all of your traffic is routed through that server. This means that your Internet service provider (ISP) can no longer see what you're doing online.

VPN servers can be used to access region-restricted websites, shield your browsing activity from prying eyes on public Wi-Fi, and more.

## How to Set Up a VPN Server

There are many different ways to set up a VPN server. In this article, we'll show you how to set up a VPN server using Windows Server 2016.

### 1. Install Windows Server 2016

If you don't already have a server, you'll need to purchase and install Windows Server 2016. You can find instructions for doing this here.

### 2. Configure the Network Adapter

Once you have Windows Server 2016 installed, you'll need to configure the network adapter. You can do this by going to the Control Panel and opening Network and Sharing Center.

Click on Change adapter settings and then right-click on the network adapter you want to configure. Select Properties from the menu.

In the Properties window, select the Internet Protocol Version 4 (TCP/IPv4) option and click the Properties button.

In the IPv4 Properties window, select the Use the following IP address option and enter the IP address, Subnet mask, and Default gateway that you want to use.

Click the OK button to save the changes.

### 3. Set Up DNS

The next step is to set up DNS. DNS is a system that allows you to use easy-to-remember domain names (like www.example.com) instead of hard-to-remember IP addresses (like 192.168.1.1).

You can set up DNS on your server by going to the Control Panel and opening the DNS Manager.

In the DNS Manager, right-click on the DNS server and select the Properties option from the menu.

In the DNS Server Properties window, select the Forwarders tab.

Click the Edit button and enter the IP address of the DNS server that you want to use. You can find a list of public DNS servers here.

Click the OK button to save the changes.

### 4. Install the Routing and Remote Access Service

The next step is to install the Routing and Remote Access Service (RRAS). RRAS is a Microsoft service that allows you to set up a VPN server.

You can install RRAS by going to the Server Manager and selecting the Add Roles and Features option.

In the Add Roles and Features wizard, select the role-based or feature-based installation option and click the Next button.

On the Select Features page, select the Remote Access checkbox and click the Next button.

On the Confirm installation selections page, click the Install button.

Once the installation is complete, click the Close button.

### 5. Configure RRAS

Now that RRAS is installed, you'll need to configure it. You can do this by going to the Server Manager and selecting the Tools option.

From the Tools menu, select the Routing and Remote Access option.

In the Routing and Remote Access console, right-click on the server and select the Configure and Enable Routing and Remote Access option.

In the Configuration Wizard, select the Custom configuration option and click the Next button.

On theCustom configuration page, select the VPN access, NAT, and LAN routing checkboxes and click the Next button.

On the Summary page, click the Finish button.

### 6. Create a VPN User

The next step is to create a user that will be allowed to connect to the VPN server. You can do this by going to the Server Manager and selecting the Tools option.

From the Tools menu, select the Active Directory Users and Computers option.

In the Active Directory Users and Computers console, right-click on the Users folder and select the New User option from the menu.

In the New User window, enter the Username, Full name, and Description for the user.

Click the Next button.

On the Password page, enter the password for the user and click the Next button.

On the Confirm password page, click the Finish button.

### 7. Configure VPN Access

The next step is to configure VPN access for the user. You can do this by going to the Server Manager and selecting the Tools option.

From the Tools menu, select the Routing and Remote Access option.

In the Routing and Remote Access console, expand the server and click on the Remote Access Policies option.

In the Remote Access Policies window, right-click on the Connections to Microsoft Routing and Remote Access server and select the Properties option from the menu.

In the Connections to Microsoft Routing and Remote Access server Properties window, select the Users tab.

Click the Add button and select the user that you want to allow to connect to the VPN server.

Click the OK button to save the changes.

### 8. Configure VPN Client

The final step is to configure the VPN client on the device that you want to connect to the VPN server.

There are many different VPN clients available, but we'll be using the built-in Windows VPN client.

To configure the VPN client, go to the Control Panel and open the Network and Sharing Center.

Click the Set up a new connection or network option.

In the Set up a connection or network window, select the Manually connect to a network option and click the Next button.

On the Connection Properties page, enter the VPN connection information. This includes the VPN type (IKEv2), the VPN server address, the VPN username, and the VPN password.

Click the Create button.

The VPN connection will now be listed in the Network and Sharing Center.

To connect to the VPN server, right-click on the connection and select the Connect option from the menu.

Enter the VPN username and password when prompted and click the Connect button.

You should now be connected to the VPN server.