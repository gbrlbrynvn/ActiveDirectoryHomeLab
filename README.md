<h1>Setting up an Active Directory Home Lab</h1>

<h2>Description</h2>
This project consists of creating a virtual environment with an Active Directory using Oracle VirtualBox. This helped me develop my skills and understanding of how Active Directory and Windows Networking work. It also furthered my knowledge on PowerShell scripting, specifically for Active Directory. My goal was to recreate the following network diagram in this sandbox environment:
<img src="https://imgur.com/Q2JTdWn.png" height="80%" width="80%" alt="Network Diagram"/>
<br />
- <b>Setup a Domain Controller that will house Active Directory and assign two network adapters, to be used to connect to the internet and for the private network, respectively </b> <br />
- <b>Set up Remote Acess Server(RAS) features to support NAT/PAT </b> <br />
- <b>Implement and maintain Windows DNS and DHCP services </b> <br />
- <b>Use PowerShell: to automate provisions of thousands of users, maintain, and deprovision user accounts.</b> <br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Oracle Virtual Box</b>

<h2>Environments Used </h2>

- <b>Windows 10 (21H2)</b>
- <b>Server 2019</b>

<h2>Program walk-through:</h2>

<p align="center">
First is create the virtual machine on Oracle VirtualBox for our Domain Controller: <br/>
<img src="https://i.imgur.com/BGDjtlu.png" height="80%" width="80%"/>
<br />
<br />
Make sure NAT and Interal Network are configured for its network adapters:  <br/>
<img src="https://i.imgur.com/PKbTLCq.png" height="40%" width="40%"/>
<img src="https://i.imgur.com/RGWFV0R.png" height="40%" width="40%"/>
<br />

Once configured, rename the network adapters respectively, while setting the Internal network adapter's IP address to 176.16.0.1, <br/>and rename the system to DController:  <br/>
<img src="https://i.imgur.com/BaAasHI.png" height="40%" width="40%"/>
<img src="https://i.imgur.com/Cgfpsf0.png" height="40%" width="40%"/>
<br />  
<br />
Using the Server Manager, add Active Directory Domain Services in the <i>Add Roles and Features</i> and use <i>gabsdomain.com</i> as the domain name:  <br/>
<img src="https://i.imgur.com/U9obxWx.png" height="40%" width="40%"/>
<img src="https://i.imgur.com/IwcO2f4.png" height="40%" width="40%"/>
<br />  
<br />
Under Windows Administrative Tools, navigate to Active Directory Users and Computers<br/> and create a new Organizational unit named _ADMIN in <i>gabsdomain.com</i>: <br/>
<img src="https://i.imgur.com/WbpbSWK.png" height="80%" width="80%"/>
<br />
<br />
Add and configure an admin user as a member of _ADMIN, then sign out and sign in using said credentials:  <br/>
<img src="https://i.imgur.com/OdSru4d.png" height="40%" width="40%"/>
<img src="https://i.imgur.com/pHACkLE.png" height="40%" width="40%"/>
<br />  
<br />
Using the Server Manager again, add Remote Access features and configure for the network interfaces for NAT:<br/>
<img src="https://i.imgur.com/qEmoZor.png" height="40%" width="40%"/>
<img src="https://i.imgur.com/rT2wDQB.png" height="40%" width="40%"/>
<br />  
<br />
Then add DHCP features and configure the IP range settings for the DHCP server, following the network diagram earlier:<br/>
<img src="https://i.imgur.com/9dEhsuk.png" height="40%" width="40%"/>
<img src="https://i.imgur.com/KsaGdYG.png" height="40%" width="40%"/>
<br />  
<br />
Now that our Domain Controller is all set up, we will use a PowerShell script to automate the provision of 1000 users:<br/>
<i>I'll further explain all the details of these PowerShell scripts in [<b>this repo!</b>](https://github.com/gbrlbrynvn/test)</i><br/>
<img src="https://i.imgur.com/65RQttv.png" height="40%" width="40%"/>
<img src="https://i.imgur.com/28pPRgC.png" height="40%" width="40%" />
<br />  
<br />
The next step for our sandbox environment is to create a Client virtual machine and configure its network adapter to Internal Network:<br/>
<img src="https://i.imgur.com/Hi3DLJD.png" height="40%" width="40%"/>
<img src="https://i.imgur.com/Pc0TDkn.png" height="40%" width="40%"/>
<br />  
<br />
Confirm that the client was automatically given an IP Address within the DHCP scope and test the connection to the internet and the Domain Controller: <br/>
<img src="https://i.imgur.com/864eXLw.png" height="80%" width="80%"/>
<br />
<br />
Change the Client PC's system name and configure to be a member of <i>gabsdomain.com</i> using the credentials created from the previous PowerShell script, then relogin:<br/>
<img src="https://i.imgur.com/fD7ozsQ.png" height="40%" width="40%"/>
<img src="https://i.imgur.com/KON914L.png" height="40%" width="40%"/>
<br />  
<br />
Using the Domain Controller's VM, confirm that the Client's PC has joined the domain: <br/>
<img src="https://i.imgur.com/Lhca7E7.png" height="40%" width="40%"/>
<img src="https://i.imgur.com/CXG0pyt.png" height="40%" width="40%"/>
<br />  
<br />
<b>This project is easily scalable and will be further improved upon and used for future projects.</b>
</p>
