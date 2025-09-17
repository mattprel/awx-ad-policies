# awx-ad-policies
An Ansible AWS repo for deploying Active Directory GPO-like policies to domain-joined Linux machines.

## List of Modifications Made to Licenced Files
Some files used in this repository are modified versions of existing files released under the GNU GPLv3.0. As a result, we are required to explicitly document any modifications made to such files. Hence, below are a list of modifications made to pre-existing licenced files used in this repository.

### [ldap_inventory.py](https://github.com/mattprel/awx-ad-policies/tree/main/plugins/inventory/ldap_inventory.py)

#### Modification 1 - Bug fix that stops the parsing loop dying when (seemingly) an OU does not contain any objects.
Line changed: `ouGroups = self._detect_group(item[0])`

Line changed to: 

    ouGroups = self._detect_group(item[0])
  
    if not ouGroups:
      display.debug("DEBUG: No OU groups detected for %s, skipping" % hostName)
      continue


### [ldap_inventory.py](https://github.com/mattprel/awx-ad-policies/tree/main/plugins/inventory/ldap_inventory.py)

#### Modification 2 - Bug fix to ensure that calculated FQDNs are NETBIOS compatible.
Line changed:

    if self.use_fqdn is True :
        domainName = "." + item[0].split('DC=',1)[1].replace(',DC=','.')
        hostName = hostName + domainName.lower()

Line changed to: 

    def to_netbios_name(name: str) -> str:
        """
        Convert a hostname to NetBIOS-compatible form:
        - Allow only alphanumeric and hyphen
        - Truncate to 15 chars (NetBIOS limit)
        - Lowercase for DNS
        """
        # Replace invalid chars with nothing
        cleaned = re.sub(r'[^A-Za-z0-9-]', '', name)
        # Truncate to 15 chars
        shortened = cleaned[:15]
        return shortened.lower()
               
    if self.use_fqdn is True:
        domainName = "." + item[0].split('DC=', 1)[1].replace(',DC=', '.')
        hostName = to_netbios_name(hostName) + domainName.lower()
