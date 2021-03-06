
###########
makehosts.8
###########

.. highlight:: perl


****
NAME
****


\ **makehosts**\  - sets up /etc/hosts from the xCAT hosts table.


********
SYNOPSIS
********


\ **makehosts**\  [\ **-n**\ ] [\ *noderange*\ ] [\ **-l**\ |\ **--longnamefirst**\ ] [\ **-d**\ ] [\ **-m**\ |\ **--mactolinklocal**\ ]

\ **makehosts**\  {\ **-h**\ |\ **--help**\ }


***********
DESCRIPTION
***********


\ **makehosts**\  updates the /etc/hosts file based on information stored in the 
xCAT database object definitions.

The main three bits of information needed are: node hostname, node ip and network domain name.

The hostname and ip address are specified as part of the node definition.

The domain value is taken either from the xCAT network definition associated with the node or from the cluster site definition.  If you are using multiple domains in the cluster you should add the domain names to the appropriate xCAT network definition.

Note: If your node hostnames and IP addresses follow a regular pattern, you can use just a few regular expressions to generate /etc/hosts using makehosts. For details on using regular expressions see the "xcatdb" man page.

If you specify additional network interfaces in your xCAT node definitions they will also be added to the /etc/hosts file.  You can specify additional network interface information (NICs) using the following node attributes: nicips, nichostnamesuffixes, nictypes, niccustomscripts, nicnetworks.  You can get a description of these attributes by running "lsdef -t node -h | more" or "man nics".


*******
OPTIONS
*******



\ **-n**\ 
 
 Completely replace the /etc/hosts file, losing any previous content.  If this option is not specified,
 it will only replace the lines in the file that correspond to the nodes in the specified noderange.
 


\ **-l**\ |\ **--longnamefirst**\ 
 
 The FQDN (Fully Qualified Domain Name) of the host will appear before the PQDN (Partially Qualified Domain Name) for each host in the /etc/hosts file.
 The default is PQDN first.
 After xCAT is installed, the attribute name "FQDNfirst" can be added into "site" table manually.  If the value is set as "1", "yes" or "enable", the /etc/hosts entries generated by "makehosts" will put the FQDN before the PQDN.  Otherwise, the original behavior will be performed.
 


\ **-m**\ |\ **--mactolinklocal**\ 
 
 Updates /etc/hosts file with IPv6 link local addresses, the link local address is generated 
 from the mac address stored in mac table.
 


\ **-d**\ 
 
 Delete rather than create records. This will also delete any additional network interfaces (NICs) included in the node definitions.
 



********
EXAMPLES
********



\*
 
 Add entries to /etc/hosts for all nodes included in the xCAT node group called "compute".
 
 
 .. code-block:: perl
 
    makehosts compute
 
 


\*
 
 If the xCAT hosts table contains:
 
 
 .. code-block:: perl
 
    "compute","|node(\d+)|1.2.3.($1+0)|","|(.*)|($1).cluster.net|",,
 
 
 Assuming the group "compute" contains node01, node02, etc., then in /etc/hosts they will be given
 IP addresses of 1.2.3.1, 1.2.3.2, etc.
 



********
SEE ALSO
********


hosts(5)|hosts.5, makedns(8)|makedns.8

