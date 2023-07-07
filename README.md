# Configuring active directory


<h3>To setup an active directory, we need a Domain controller and a Client. For the domain controller in azure, setup the operating system as "Windows server 2022 Datacenter"</h3>

![image](https://github.com/David123890dd/configure-ad/assets/138183500/7144cbaf-66f7-4089-b3f0-cd5db03ab13b)

<h3>We need to make the IP adressing for the Domain controller static. To do that, go to the domain controller --> Networking --> Network Interface --> IP configurations --> ipconfig1 and set it to static and save. before launching the client, make sure to restart the virtual machine</h3>

![image](https://github.com/David123890dd/configure-ad/assets/138183500/07fbadc3-73de-4e64-b5c0-31cfb51ed1d5)


<h3>for the client virtual machine, Under the networking section, set the virtual network the same as domain controller's network</h3>

![image](https://github.com/David123890dd/configure-ad/assets/138183500/ec6e0932-ec0f-4c63-b1bc-87bd210eb7c4)

<h3>Set the client DNS server to the domain controller NIC private IP. To do that, go to the client virtual machine, Networking --> Network interface --> DNS Servers --> Custom and type in the Private DNS numbers found in Domain controller, Networking. you will see the NIC private IP</h3>

![image](https://github.com/David123890dd/configure-ad/assets/138183500/ac9ce6db-0b0a-4d57-b1ef-fe8d99ef79db)

![image](https://github.com/David123890dd/configure-ad/assets/138183500/40a3a8c6-dd4d-4c4b-ae99-bd86f6c1255b)

<h3>Connect to the domain controller, in server manager, click "Add roles and features"</h3>

![image](https://github.com/David123890dd/configure-ad/assets/138183500/f4b7e081-e236-4b76-820c-1fb27a8fbffc)

<h3>click Next --> Next --> Next --> check "Active Directory Domain Services" --> "Add Features" --> Next --> Next --> Next --> Install</h3>

![image](https://github.com/David123890dd/configure-ad/assets/138183500/9a27f446-5e85-4336-886f-61b5562d5f75)

<h3>after the installation, click on the flag and click "Promote this server to a domain controller"</h3>

![image](https://github.com/David123890dd/configure-ad/assets/138183500/8e94b604-8149-4399-aeb3-39384427a7c1)

<h3>Click "Add a new forest" and create a domain name. The name will be used again so remember it</h3>

![image](https://github.com/David123890dd/configure-ad/assets/138183500/8e3f7752-a03a-45f2-b88f-fb81e50886f7)

<h3>Set the password for the Directory Service Restore Mode(DSRM), Next --> Next --> Next --> Next --> Next --> Install. Once installed the Domain controller will Restart or shutdown</h3>

![image](https://github.com/David123890dd/configure-ad/assets/138183500/47710f5a-c18a-44c1-9fce-a7f3b652416c)

<h3>From now on, when connecting to the Domain controller, log in with the root domain name, type backslash and the Domain controller's Username. The password is the same. Go to "more choices" --> "Use a Different Account" </h3>

![image](https://github.com/David123890dd/configure-ad/assets/138183500/528bc133-d1ee-4038-81bb-009d85146a4e)

<h3>Now let's connect the client to the Domain. Open the client virtual machine, go to settings --> System --> About --> "Rename this PC(Advanced)" --> "Change..."</h3>

![image](https://github.com/David123890dd/configure-ad/assets/138183500/197fe9dc-242d-4acd-b3ad-0daf1c073cf4)

<h3>Under "Member of", click "Domain" and enter the root domain name. After that, type in the new login info that we use in the domain controller. Restart your virtual machine. Now we are connected to the domain. We just need to allow everyone in the domain to have access to the client.</h3>

![image](https://github.com/David123890dd/configure-ad/assets/138183500/2eddf0b1-a5bf-42a9-809a-270991b408dd)

<h3>Log back in, go to ssettings --> System --> Remote Dekstop --> Select users that can remotely access this PC</h3>

![image](https://github.com/David123890dd/configure-ad/assets/138183500/9eef694a-541a-4522-ac2a-7246212b2e54)

<h3>Click "add..." and enter "Domain Users". Fill in the new domain controller's login credentials and you should see this:</h3>

![image](https://github.com/David123890dd/configure-ad/assets/138183500/7c6d299c-a83f-40cd-902e-99ade0e61bdd)

<h3>CLick "ok". Now everything is setup. Now we just need to create domain user account(s) and test it out. Go back to the Domain controller and in the "Server manager" application, go to "tools" --> "Active Directory Users and Computers"</h3>

![image](https://github.com/David123890dd/configure-ad/assets/138183500/1f7e20ce-fa43-4f5c-894d-d09a192d3b34)

<h3>Go to MD.com, right click it and select new --> Organizational unit. This will be the folder we will put our users in</h3>

![image](https://github.com/David123890dd/configure-ad/assets/138183500/750a4a13-3d5b-4910-b29d-10ed5a8aba9b)

<h3>in the folder we created, right click --> New --> user. fill in their login info. The "user logon name" is what will be used as the login credentials when connecting to any of the computers connected to the domain controller. Click next --> setup password --> next --> finish. Now we have a domain user.</h3>

![image](https://github.com/David123890dd/configure-ad/assets/138183500/8cf83bea-a709-4709-8c82-c3b276c7e702)

<h3>Enter the login info we created for the user in our client virtual machine. without a domain controller, we wouldn't be able to log in becuase we never created an account for that user. Since we are connected to the domain, any account created under the domain, can be used to login in any computer if the computer is connected to the domain.</h3>
