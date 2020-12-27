#!/bin/bash

############################################################################
# Squid Proxy Installer (SPI)                                              #
# Version: 2.0 Build 2017                                                  #
# Branch: Stable                                                           #
#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~#
# Author: Hidden Refuge (© 2014 - 2017)                                    #
# Modified for me: Icharis, Thanks to hidden-refuge for leading the    #
# way.	and thanks to ADHD-- copied from his repo           		   #
# License: MIT License                                                     #
#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~#
# GitHub Repo: https://github.com/hidden-refuge/spi/                       #
# SPI Wiki: https://github.com/hidden-refuge/spi/wiki                      #
############################################################################

# Declaring a few misc variables
vspiversion=2.0 # SPI version
vspibuild=2017 # SPI build number
vbranch=Stable # SPI build branch
vsysarch=$(getconf LONG_BIT) # System architecture

# Function for iptables rules (CentOS 5 & 6)
firew1 ()	{
	# Opening default Squid port 3128 for clients to connect
	iptables -I INPUT -p tcp --dport 3128 -j ACCEPT
	# Saving firewall rules
	service iptables save
}

# Function for iptables rules (CentOS 7, Debian, Ubuntu, Fedora)
firew2 ()	{
	# Opening default Squid port 3128 for clients to connect
	iptables -I INPUT -p tcp --dport 3128 -j ACCEPT
	# Saving firewall rules
	iptables-save
}

# Function for RHEL 5 Linux distributions
rhel5 ()	{
	# Downloading and installing necessary repo for newer Squid 3 versions for CentOS 5
	rpm -Uvh http://flexbox.sourceforge.net/centos/5/i386/flexbox-release-1-4.3.noarch.rpm
	# Installing necessary packages (Squid, httpd for htpasswd and dependencies)
	yum install perl-DBI libecap squid httpd -y
	# Asking user to set a username via read and writing it into $usrn
	read -e -p "Your desired username: " usrn
	# Creating user with username from $usrn and asking user to set a password
	htpasswd -c /etc/squid/passwd $usrn
	# Downloading necessary Squid.conf for the corresponding OS & system architecture
	case $vsysarch in
			32) # 32 bit Squid configuration
					wget -O /etc/squid/squid.conf https://raw.githubusercontent.com/icharisofcc/proxy/master/spi-rhel5632.conf --no-check-certificate;;
			64) # 64 bit Squid configuration
					wget -O /etc/squid/squid.conf https://raw.githubusercontent.com/icharisofcc/proxy/master/spi-rhel5664.conf --no-check-certificate;;
	esac
	# Creating empty blacklist.acl file for further blacklisting entries
	touch /etc/squid/blacklist.acl
	# Restarting Squid and enabling its service
	service squid restart && chkconfig squid on
	# Turning off httpd and removing it from services (post installation of yum enabled it but we don't need it)
	service httpd stop && chkconfig httpd off
	# Running function firew1
	firew1
}

# Function for RHEL 6 Linux distributions
rhel6 ()	{
	# Installing necessary packages (Squid, httpd-tools for htpasswd and dependencies)
	yum install squid httpd-tools -y
	# Asking user to set a username via read and writing it into $usrn
	read -e -p "Your desired username: " usrn
	# Creating user with username from $usrn and asking user to set a password
	htpasswd -c /etc/squid/passwd $usrn
	# Downloading necessary Squid.conf for the corresponding OS & system architecture
	case $vsysarch in
			32) # 32 bit Squid configuration
					wget -O /etc/squid/squid.conf https://raw.githubusercontent.com/icharisofcc/proxy/master/spi-rhel5632.conf --no-check-certificate;;
			64) # 64 bit Squid configuration
					wget -O /etc/squid/squid.conf https://raw.githubusercontent.com/icharisofcc/proxy/master/spi-rhel5664.conf --no-check-certificate;;
	esac
	# Creating empty blacklist.acl file for further blacklisting entries
	touch /etc/squid/blacklist.acl
	# Restarting Squid and enabling its service
	service squid restart && chkconfig squid on
	# Running function firew1
	firew1	
}

# Function for RHEL 7 Linux distributions
rhel7 ()	{
	# Installing necessary packages (Squid, httpd-tools for htpasswd and dependencies)
	yum install nano dos2unix squid httpd-tools -y
	# Asking user to set a username via read and writing it into $usrn
	read -e -p "Your desired username: " usrn
	# Creating user with username from $usrn and asking user to set a password
	htpasswd -c /etc/squid/passwd $usrn
	# Downloading Squid configuration 
	wget -O /etc/squid/squid.conf https://raw.githubusercontent.com/icharisofcc/proxy/master/spi-rhel7.conf --no-check-certificate
	# Creating empty blacklist.acl file for further blacklisting entries
	touch /etc/squid/blacklist.acl
	# Restarting Squid and enabling its service
	systemctl restart squid.service && systemctl enable squid.service
	# Running function firew2
	firew2
}

# Function for Debian "Squeeze" 6 and Debian "Wheezy" 7
deb ()	{
	# Updating package database
	apt-get update
	# Installing necessary packages (Squid, apache2-utils for htpassword and dependencies)
	apt-get install apache2-utils squid3 -y
	# Asking user to set a username via read and writing it into $usrn
	read -e -p "Your desired username: " usrn
	# Creating user with username from $usrn and asking user to set a password
	htpasswd -c /etc/squid3/passwd $usrn
	# Downloading Squid configuration
	wget -O /etc/squid3/squid.conf https://raw.githubusercontent.com/icharisofcc/proxy/master/spi-debian.conf --no-check-certificate
	# Creating empty blacklist.acl file for further blacklisting entries
	touch /etc/squid3/blacklist.acl
	# Restarting Squid and enabling its service
	service squid3 restart && update-rc.d squid3 defaults
	# Running function firew2
	firew2
}

# Function for Debian "Jessie" 8
deb8 ()	{
	# Updating package database
	apt-get update
	# Installing necessary packages (Squid, apache2-utils for htpassword and dependencies)
	apt-get install apache2-utils squid3 -y
	# Asking user to set a username via read and writing it into $usrn
	read -e -p "Your desired username: " usrn
	# Creating user with username from $usrn and asking user to set a password
	htpasswd -c /etc/squid3/passwd $usrn
	# Downloading Squid configuration
	wget -O /etc/squid3/squid.conf https://raw.githubusercontent.com/icharisofcc/proxy/master/spi-jessie.conf --no-check-certificate
	# Creating empty blacklist.acl file for further blacklisting entries
	touch /etc/squid3/blacklist.acl
	# Restarting Squid and enabling its service
	service squid3 restart && update-rc.d squid3 defaults
	# Running function firew2
	firew2
}

# Function for Ubuntu User Auth
ubt ()	{
	# Updating package database
	apt-get update
	# Installing necessary packages (Squid, apache2-utils for htpassword and dependencies)
	apt-get install nano dos2unix apache2-utils squid3 -y
	# Asking user to set a username via read and writing it into $usrn
	read -e -p "Your desired username: " usrn
	# Creating user with username from $usrn and asking user to set a password
	htpasswd -c /etc/squid3/passwd $usrn
	# Downloading Squid configuration
	wget -O /etc/squid3/squid.conf https://raw.githubusercontent.com/icharisofcc/proxy/master/spi-ubuntu.conf --no-check-certificate
	# Copying squid3.conf from init to init.d for startup script
	cp /etc/init/squid3.conf /etc/init.d/squid3
	# Creating empty blacklist.acl file for further blacklisting entries
	touch /etc/squid3/blacklist.acl	
	# Restarting Squid and enabling its service
	service squid3 restart && update-rc.d squid3 defaults
	# Running function firew2
	firew2
}

# Function for Ubuntu Ip Auth
ubt_ip ()	{
	# Updating package database
	apt-get update
	# Installing necessary packages (Squid, apache2-utils for htpassword and dependencies)
	apt-get install nano dos2unix apache2-utils squid3 -y
	# Asking user to set a username via read and writing it into $usrn
	# read -e -p "Your desired username: " usrn
	# Creating user with username from $usrn and asking user to set a password
	# htpasswd -c /etc/squid3/passwd $usrn
	# Downloading Squid configuration
	wget -O /etc/squid3/squid.conf https://raw.githubusercontent.com/icharisofcc/proxy/master/spi-ubuntu_ip_auth.conf --no-check-certificate
	# Copying squid3.conf from init to init.d for startup script
	cp /etc/init/squid3.conf /etc/init.d/squid3
	# Creating empty blacklist.acl file for further blacklisting entries
	touch /etc/squid3/blacklist.acl
	# Restarting Squid and enabling its service
	service squid3 restart && update-rc.d squid3 defaults
	# Running function firew2
	firew2
}

# Function for Ubuntu No Auth
ubt_null ()	{
	# Updating package database
	apt-get update
	# Installing necessary packages (Squid, apache2-utils for htpassword and dependencies)
	apt-get install nano dos2unix apache2-utils squid3 -y
	# Asking user to set a username via read and writing it into $usrn
	# read -e -p "Your desired username: " usrn
	# Creating user with username from $usrn and asking user to set a password
	# htpasswd -c /etc/squid3/passwd $usrn
	# Downloading Squid configuration
	wget -O /etc/squid3/squid.conf https://raw.githubusercontent.com/icharisofcc/proxy/master/spi-ubuntu_no_auth.conf --no-check-certificate
	# Copying squid3.conf from init to init.d for startup script
	cp /etc/init/squid3.conf /etc/init.d/squid3
	# Creating empty blacklist.acl file for further blacklisting entries
	touch /etc/squid3/blacklist.acl
	# Restarting Squid and enabling its service
	service squid3 restart && update-rc.d squid3 defaults
	# Running function firew2
	firew2
}

# Function for Fedora
fed () {
	# Installing necessary packages (Squid, httpd-tools for htpasswd and dependencies)
	yum install squid httpd-tools -y
	# Asking user to set a username via read and writing it into $usrn
	read -e -p "Your desired username: " usrn
	# Creating user with username from $usrn and asking user to set a password
	htpasswd -c /etc/squid/passwd $usrn
	# Downloading necessary Squid.conf for the corresponding OS & system architecture
	case $vsysarch in
		32) # 32 bit Squid configuration
			wget -O /etc/squid/squid.conf https://raw.githubusercontent.com/icharisofcc/proxy/master/spi-fedora32.conf --no-check-certificate;;
		64) # 64 bit Squid configuration
			wget -O /etc/squid/squid.conf https://raw.githubusercontent.com/icharisofcc/proxy/master/spi-rhel7.conf --no-check-certificate;;
	esac
	# Creating empty blacklist.acl file for further blacklisting entries
	touch /etc/squid/blacklist.acl
	# Restarting Squid and enabling its service
	systemctl restart squid && systemctl enable squid
	# Running function firew2
	firew2
}

# Default function with information
dinfo ()	{
	echo "Squid Proxy Installer $vspiversion Build $vspibuild"
	echo "You are using builds from the $vbranch branch"
	echo ""
	echo "Usage: bash spi <option>"
	echo "Example (Debian 8): bash spi -jessie"
	echo ""
	echo "Options:"
	echo "-rhel5   -- RHEL 5 Linux distributions such as Red Hat 5, CentOS 5 and et cetera"
	echo "-rhel6   -- RHEL 6 Linux distributions such as Red Hat 6, CentOS 6 and et cetera"
	echo "-rhel7   -- RHEL 7 Linux distributions such as Red Hat 7, CentOS 7 and et cetera"
	echo "-debian  -- Debian Squeeze 6 & Wheezy 7"
	echo "-jessie  -- Debian Jessie 8"
	echo "-ubuntu  -- Ubuntu"
	echo "-fedora  -- Fedora"
	echo ""
	echo "How to add more users:"
	echo "https://github.com/hidden-refuge/spi/wiki/User-management"
	echo ""
	echo "How to blacklist domains:"
	echo "https://github.com/hidden-refuge/spi/wiki/Domain-blacklist"
	echo ""
	echo ""
	echo "(C) 2014 - 2017 by Hidden Refuge"
	echo "GitHub Repo: https://github.com/hidden-refuge/spi"
	echo "SPI Wiki: https://github.com/hidden-refuge/spi/wiki"
}

# Checking $1 and running corresponding function
case $1 in
	'-rhel5') # If option "-rhel5" run function rhel5
		rhel5;; # RHEL 5 Linux distributions such as Red Hat 5, CentOS 5 and et cetera
	'-rhel6') # If option "-rhel6" run function rhel6
		rhel6;; # RHEL 6 Linux distributions such as Red Hat 6, CentOS 6 and et cetera
	'-rhel7') # If option "-rhel7" run function rhel7
		rhel7;;	# RHEL 7 Linux distributions such as Red Hat 7, CentOS 7 and et cetera
	'-debian') # If option "-debian" run fuction deb
		deb;; # Debian "Squeeze" 6 and Debian "Wheezy" 7
	'-jessie') # If option "-jessie" run function deb8
		deb8;; # Debian "Jessie" 8
	'-ubuntu') # If option "-ubuntu" run function ubt
		ubt;; # Ubuntu User
	'-ubuntu_ip') # If option "-ubuntu_ip" run function ubt_ip
		ubt_ip;; # Ubuntu Ip		
	'-ubuntu_null') # If option "-ubuntu" run function ubt_null
		ubt_null;; # Ubuntu	Null
	'-fedora') # If option "fedora" run function fed
		fed;; # Fedora 
	*) # If option empty or non existing run function info
		dinfo;; # Default, information about available options and et cetera
esac
