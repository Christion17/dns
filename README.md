<p align="center">
<img src="https://i.imgur.com/Iyloxet.png" height = 20% width = 20%/>
</p>

<h1 align = "center">Understanding & Building Intuition for DNS (Domain Name System)</h1>
This lab demonstrates the use of DNS and how to configure it. DNS serves as the phonebook of the Internet, translating domain names to IP addresses so browsers can load Internet resources (essentially why we don't need to type IP addresses to access Google.com). To see how it works in practice, this lab follows up from the <a href = "https://github.com/Christion17/active-directory">installation and configuration of an Active Directory</a>. When configured and installed, we'll perform excercises with the client and domain controller virtual machines in order to understand DNS a bit better.

<br />

<h2>Environments and Technologies Used</h2>
<ul>
  <li>Microsoft Azure (Virtual Machines/Compute)</li>
  <li>Remote Desktop</li>
  <li>Active Directory Domain Services</li>
  <li>Command Prompt</li>
</ul>

<br />

<h2>Operating Systems Used</h2>
<ul>
  <li>Windows Server 2022</li>
  <li>Windows 10 Pro (21H2)</li>
</ul>

<br />

<h2>DNS Exercises</h2>

<!-- <img src = "" width = 80% height = 80% /> -->

<h3>A-Record</h3>

<p>
  <ul>
    <li>The "A" in A-Record stands for "address" and this is the most fundamental type of DNS record: pointing to the name of the IP address of a given domain.</li>
    <li>Connect and log in to your Domain Controller and Client virtual machines as admins <b>(mydomain.com\jane_admin)</b></li>
    <li>In the Client VM, open up Command Prompt and attempt to ping "mainframe" by entering the command <b>ping mainframe</b>; you will notice it will fail</li>
    <ul>
      <li><img src = "https://i.imgur.com/JsHo3Hr.png" width = 80% height = 80% /></li>
    </ul>
    <li>The same result also applies if we attempt and nslookup of the mainframe (command line <b>nslookup mainframe</b>) because we do not have a DNS record</li>
    <li>To create a DNS A-Record, go to the Domain Controller VM and open the <b>DNS Manager</b>b> in the Server Manager Board and go to the domain you created within the <b>Forward Lookup Zones</b> tab (mydomain.com)</li>
    <li>Right click on the page and create a <b>New Host (A or AAAA)</b>. We will name the host <b>mainframe</b> and the IP address should be the same IP as the domain controller so that ping can resolve. Once the information is entered, click <b>Add Host</b> and refresh the DNS server so that the new record can be updated.</li>
    <ul>
      <li><img src = "https://i.imgur.com/KegPYuO.png" width = 80% height = 80% /></li>
    </ul>
    <li>Head back to the Client VM and attempt to ping the mainframe again, the issue should be resolved and receive the ping successfully</li>
    <ul>
      <li><img src = "https://i.imgur.com/RYv6zMQ.png" width = 80% height = 80% /></li>
      <li>Performing an nslookup</li>
      <li><img src = "https://i.imgur.com/mA1dM7A.png" width = 80% height = 80% /></li>
    </ul>
  </ul>
</p>

<br />

<h3>Local DNS Cache</h3>

<p>
  <ul>
    <li>This showcases a DNS cache by creating a local DNS</li>
    <li>In the Domain Controller VM, go back to the <b>DNS Manager</b> and locate the mainframe host we've created and edit the IP address to <b>8.8.8.8</b></li>
    <ul>
      <li><img src = "https://i.imgur.com/xavbiEl.png" width = 80% height = 80% /></li>
    </ul>
    <li>Back to the Client VM, ping the mainframe and you'll notice it pings the mainframe's old IP address and not 8.8.8.8. This is because the cache needs to be updated, more evidence of how it is the old cache is if we entered the command <b>ipconfig /displaydns</b></li>
    <ul>
      <li><img src = "https://i.imgur.com/MGn9Vtv.png" width = 80% height = 80% /></li>
    </ul>
    <li>Still in the Client VM, run Command Prompt as Administrator and enter the command <b>ipconfig /flushdns</b> (it's a <i>very</i> helpful command for flushing the DNS for testing pings in IT) and observe the cache is now empty</li>
    <ul>
      <li><img src = "https://i.imgur.com/ZycFn8d.png" width = 80% height = 80% /></li>
    </ul>
    <li>Attempt to ping mainframe again, and now the new record should appear</li>
    <ul>
      <li><img src = "https://i.imgur.com/igUKeqH.png" width = 80% height = 80% /></li>
    </ul>
  </ul>
</p>

<br />

<h3>CNAME Record</h3>

<p>
  <ul>
    <li>"CNAME" is abbreviated form of "Canonical Name:" pointing to a name to another name instead of to an IP address unlike A-Record</li>
    <li>In the Domain Controller VM, open the <b>DNS Manager</b>b> in the Server Manager Board and go to the domain you created within the <b>Forward Lookup Zones</b> tab (mydomain.com)</li>
    <li>Right click on the page and create a <b>New Alias (CNAME)</b>. We will name the alias <b>search</b> and the fully qualified domain name (FQDN) to any website such as <b>www.google.com</b>. Once the information is entered, click <b>OK</b> and refresh the DNS server so that the new record can be updated.</li>
    <ul>
      <li><img src = "https://i.imgur.com/nBVaaA6.png" width = 80% height = 80% /></li>
    </ul>
    <li>Back to the Client VM, ping the record we've named "search" by the command <b>ping search</b> and observe the results of the CNAME Record. It should ping to the website listed in the FQDN (for this case, Google)</li>
    <ul>
      <li><img src = "https://i.imgur.com/aPbBESi.png" width = 80% height = 80% /></li>
    </ul>
    <li>Performing the nslookup command with "search" (<b>nslookup search</b>) will result in an name server lookup for Google</li>
  </ul>
</p>

<br />
