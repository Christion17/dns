<p align="center">
<img src="https://i.imgur.com/Iyloxet.png" height="20%" width="20%"/>
</p>

<h1 align="center">DNS (Domain Name System) - Resolution and Caching</h1>

<p>
This project demonstrates how DNS translates domain names into IP addresses and how caching affects name resolution in a domain environment.
</p>

<p>
The objective is to understand how DNS records, caching, and aliasing (CNAME) influence system communication.
</p>

<br />

<h2>Environment</h2>
<ul>
  <li>Microsoft Azure (Virtual Machines)</li>
  <li>Windows Server 2022 (Domain Controller)</li>
  <li>Windows 10 (Client)</li>
  <li>Active Directory Domain Services</li>
  <li>Command Prompt</li>
</ul>

<br />

<h2>Core Concepts</h2>
<ul>
  <li><b>A Record</b> – Maps a hostname to an IP address</li>
  <li><b>DNS Cache</b> – Stores previous lookups locally</li>
  <li><b>CNAME</b> – Maps one domain name to another</li>
</ul>

<br />

<h2>A Record (Name Resolution)</h2>

<p>
<ul>
  <li>From the client VM, attempt to ping <b>mainframe</b></li>
  <li>Ping fails because no DNS record exists</li>
  <ul>
    <li><img src="https://i.imgur.com/JsHo3Hr.png" width="80%" height="80%" /></li>
  </ul>

  <li>Create an A Record in DNS Manager:
    <ul>
      <li>Name: <b>mainframe</b></li>
      <li>IP: Domain Controller IP</li>
    </ul>
  </li>

  <li>After creating the record, ping succeeds</li>
  <ul>
    <li><img src="https://i.imgur.com/RYv6zMQ.png" width="80%" height="80%" /></li>
  </ul>
</ul>
</p>

<br />

<h2>DNS Cache Behavior</h2>

<p>
<ul>
  <li>Modify the A Record IP address (e.g., change to <b>8.8.8.8</b>)</li>

  <li>Client still resolves the old IP due to cached DNS entry</li>
  <ul>
    <li><img src="https://i.imgur.com/MGn9Vtv.png" width="80%" height="80%" /></li>
  </ul>

  <li>Clear cache using:
    <b>ipconfig /flushdns</b></li>

  <li>After flushing, the new IP is resolved</li>
  <ul>
    <li><img src="https://i.imgur.com/igUKeqH.png" width="80%" height="80%" /></li>
  </ul>
</ul>
</p>

<br />

<h2>CNAME Record (Alias Resolution)</h2>

<p>
<ul>
  <li>Create a CNAME record:
    <ul>
      <li>Name: <b>search</b></li>
      <li>Target: <b>www.google.com</b></li>
    </ul>
  </li>

  <li>Ping <b>search</b> from the client</li>
  <li>DNS resolves to the target domain</li>
  <ul>
    <li><img src="https://i.imgur.com/aPbBESi.png" width="80%" height="80%" /></li>
  </ul>
</ul>
</p>

<br />

<h2>System Flow</h2>
<ul>
  <li>Client queries DNS → DNS returns IP address</li>
  <li>Result is stored locally in cache</li>
  <li>Cache must be cleared to reflect updated records</li>
  <li>CNAME redirects one domain name to another target</li>
</ul>

<br />

<h2>Key Takeaways</h2>
<ul>
  <li>DNS translates names into IP addresses</li>
  <li>Without DNS records, name resolution fails</li>
  <li>Cached entries can override updated records</li>
  <li>Flushing DNS forces fresh resolution</li>
  <li>CNAME records allow flexible domain redirection</li>
</ul>

<br />

<h2>What This Demonstrates</h2>
<ul>
  <li>Understanding of DNS resolution and record types</li>
  <li>Ability to troubleshoot name resolution issues</li>
  <li>Awareness of caching behavior in network systems</li>
  <li>Practical use of DNS in an Active Directory environment</li>
</ul>
