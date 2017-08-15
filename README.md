# SPI - Squid Proxy Installer
A Squid proxy installer with username and password authentication<br /><br /><br />
The Squid Proxy Installer (short: SPI) is a fully automated shell script to install an anonymous HTTP proxy based on Squid 3 with a username and password authentication through NCSA Auth and htpasswd. It requires no other input than your desired username and password. The default configuration listens on the default TCP port 3128!<br /><br />
SPI was written for the most common server Linux operating systems:
<ul>
<li>CentOS 5/6/7</li>
<li>Debian 6/7/8</li>
<li>Ubuntu (most versions are supported)</li>
<li>Fedora (most versions are supported)</li>
<li>More OS on request</li>
</ul>
64 Bit versions of some operating systems require more than 256 MB RAM for Squid to work (this includes generally Debian and Ubuntu as a outcome of various tests in OpenVZ).<br /><br /><br />
<b>How to use:</b><br /><br />
You can find installation and usage guides for all supported operating systems here:<br />
https://github.com/hidden-refuge/spi/wiki/Usage
<br /><br />
<b>How to add more users</b><br /><br />
You can easily add more users which are allowed to access your proxy with the command below:<br />
https://github.com/hidden-refuge/spi/wiki/User-management<br /><br />
<strong>Domain blacklist</strong><br /><br />
You can easily block access to domains by adding them to the "blacklist.acl" file. Follow this guide:<br />
https://github.com/hidden-refuge/spi/wiki/Domain-blacklist
<br /><br />
For help with Squid and in order to change the configuration according to your needs please consult the <a href="http://wiki.squid-cache.org/SquidFaq">Squid FAQ</a> and the <a href="http://wiki.squid-cache.org/">Squid wiki</a>.
