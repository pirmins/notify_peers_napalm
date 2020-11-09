# notify_peers_napalm

notify_peers is a BGP peering maintenance Ansible module. It sends out notification emails to peers NOCs when BGP sessions towards them are down and a summary of it all to your NOC email.

## How does it work?

Very simply, it works like this:

- ansible_notify_peers_playbook.yml:
  - imports vars from vars/config.yml
  - connects to the router via NAPALM's Ansible module to get the standardized CLI/API output equivalent of "show ip bgp summary"
  - registers the output into a variable
  - call the homemade Ansible module in library/notify_peers_napalm / takes the output as var then:
    - parses the output to get a list of peers that are down
    - goes through that string list and makes a list of peer objects
    - goes through the list of peers to fill NOC email and company name fields through peeringdb.com API calls based on ASN
    - [optional] goes through the list of peers to send a personalized E-mail to the remote ASN asking for checking the peering session
    - [optional] sends a report to your own NOC
      [/optional

## Support

For now the script supports following tested router CLI type:
- SLXOS
BUT should support all Napalm supported devices (bgp_neighbors getter) in theory.

## Todo
- may need more adjustability (option to not make any peeringdb API calls at all)
- ...

