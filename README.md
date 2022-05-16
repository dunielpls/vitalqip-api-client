# VitalQIP API Client
A Python 3.x client for the Nokia™ VitalQIP® JSON REST API.

# Can I use it?
I have no idea which versions of VitalQIP actually support this specific API, but you should be able to access it if you are able to access the `/rest-api` URL at your instance. I can however confirm that it is supported by VitalQIP version 8.1.1.


# Installation:
TODO: PyPI package.

This package can be installed in the following ways:
- Pip: `pip install --user vitalqip`
- Poetry: `poetry add vitalqip`
- From source: TODO

# Examples:
```python
from vitalqip import VitalQIP

# Format can be "json" or "xml" and is optional, defaulting to the former.
qip = VitalQIP("http://my-qip.int.example.com", "alice", "hunter2", "Allsafe Cybersecurity LLC", format="json")

# Change organization.
qip.set_organization("Evil Corp Inc")

# Get some data.
networks0 = qip.list_networks_v4() # Convenience function for performing an empty search.
networks1 = qip.search_networks_v4(
    # All of the following keyword arguments are optional.
    address="10.10.4.0",
    name="Branch Office 1",
    page_size=5,
    page_index=0
)
network = qip.get_network("datacenter-mgmt") # Name or address.

subnets0 = qip.list_subnets_v4()
subnets1 = qip.search_subnets_v4(
    # Both are optional.
    address="10.20.30.0",
    name="CE Linknet"
)
subnet = qip.get_subnet_v4("10.20.30.0") # Name or address.

addresses = qip.get_addresses_v4("192.168.1.0") # List addresses in subnet.
object = qip.get_address_v4("192.168.1.203")

exists = qip.address_exists_v4("192.168.1.204") # Boolean.
if exists:
    qip.delete_address_v4("192.168.1.204")

qip.add_address_v4({
    # See the documentation for a full list of supported properties. This method is subject to change.
    "subnetAddr": "192.168.1.0",
    "objectAddr": "192.168.1.204",
    "objectName": "webserver01",
    "domainName": "host.int.example.com",
    "objectClass": "Server"
})

qip.update_address_v4({
    "objectAddr": "192.168.1.204",
    "objectClass": "Virtual Server"
})

qip.update_addresses_v4({
    "objectAddr": [
        "192.168.1.205",
        "192.168.1.206"
    ],
    "objectClass": "Virtual Server"
})

# TODO: Move some of this to a GitHub wiki. Add concrete examples in `examples/`. DNS, DHCP and IPv6. Generic "QIP search".
```

# Docs
TODO

# Tests
TODO

# Non-affiliation disclaimer
Neither this repository nor the software contained in it is endorsed by, directly affiliated with, maintained, authorized, or sponsored by Nokia. All product and company names are the registered trademarks of their original owners.

# License
Licensed under the MIT license.
