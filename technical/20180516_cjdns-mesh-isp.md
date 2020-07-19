---
title: Mesh ISP
date: 2018-05-16
---

# mesh-isp
A model for Internet Gateway over a cjdns mesh

`Status`: This was an early-stage proposal originally located in the now archived `deployment` repository.  This document requires theoretical and practical validation. The questions we are trying to answer are:

* Is this possible?
* Is this practical?

## Internet Gateways and Clients

A feature in cjdns allows us to use the cjdns switch layer as a VPN carrier, such that the node acts as an exit node to the Internet. Here is the block of configurations from **cjdroute.conf** to set this up.

```
// System for tunneling IPv4 and ICANN IPv6 through cjdns.
// This is using the cjdns switch layer as a VPN carrier.
"ipTunnel":
{
    // Nodes allowed to connect to us.
    // When a node with the given public key connects, give them the
    // ip4 and/or ip6 addresses listed.
    "allowedConnections":
    [
        // Give the client an address on 192.168.1.0/24, and an address
        // it thinks has all of IPv6 behind it.
        // {
        //     "publicKey": "f64hfl7c4uxt6krmhPutTheRealAddressOfANodeHere7kfm5m0.k",
        //     "ip4Address": "192.168.1.24",
        //     "ip4Prefix": 24,
        //     "ip6Address": "2001:123:ab::10",
        //     "ip6Prefix": 0
        // },

        // It's ok to only specify one address.
        // {
        //     "publicKey": "ydq8csdk8p8ThisIsJustAnExampleAddresstxuyqdf27hvn2z0.k",
        //     "ip4Address": "192.168.1.25",
        //     "ip4Prefix": 24
        // }
    ],

    "outgoingConnections":
    [
        // Connect to one or more machines and ask them for IP addresses.
        // "6743gf5tw80ExampleExampleExampleExamplevlyb23zfnuzv0.k",
        // "pw9tfmr8pcrExampleExampleExampleExample8rhg1pgwpwf80.k",
        // "g91lxyxhq0kExampleExampleExampleExample6t0mknuhw75l0.k"
    ]
}
```

There are two nodes at play here: the **Internet Gateway** node, and the **Client** node.

### Internet Gateway

The Internet Gateway node takes the role of an ISP, responsible for exiting mesh traffic to the Internet for its Client nodes. To configure which clients are allowed to use this gateway, it pins the cjdns public key of the Client node to its **allowedConnections** and assigns an IP to the client.

The Internet Gateway cannot simply allow any mesh node to exit traffic through it, because exited traffic incurs upstream bandwidth cost to the Internet Gateway node. This public key pinning system allows the Internet Gateway to easily manage who its downstream clients are.

### Client

A Client node may be a friend's node connected to the mesh, or a phone that you carry out. Using the mesh as last-mile, these devices can access Internet content through their Internet Gateway node.

If order for the Client to specify its Internet Gateway, it pins the cjdns public key of the Internet Gateway node in its **outgoingConnections**.

## Anyone Can Be An ISP

From the above configuration, you can see that a Client node may have multiple Internet Gateways. In addition, a node can also be a Client to some Internet Gateways, but also an Internet Gateway to its own set of Clients!

By sharing the last-mile, we allow any node to share its upstream Internet bandwidth to its Clients. In effect, this allows anyone to become an ISP.

## Technical Validation

An ISP model based on cjdns public key pinning is described, where cjdns IP tunnel through a node is permitted for clients with their public keys added to the **allowedConnections** section of the provider's cjdns config.

The network topology may look something like this:

```
+--------------+            +------------------+
|              | Mesh Point |                  |       Wireless
|    Client    +------------+ Internet Gateway +-----> or ISP
|              |            |                  |       Uplink to
+------------+-+            +---+--------------+       Internet
             |                  |
  Mesh Point |                  |
             |                  | Mesh Point
+------------+-+                | over 2.4 GHz
|              |                |
|    Client    +----------------+
|              |
+------------+-+
             |
  Mesh Point |
             |
+------------+-+
|              |
|    Client    |
|              |
+--------------+
```

All the nodes run cjdns and has a unique IPv6 address. All these devices may be Raspberry Pi's, or other devices capable of running cjdns and support Mesh Point radios.

`Validate`: The cjdns IP tunnelling feature via IPv6 pinning.

`Validate`: How many Clients can a Raspberry Pi support as Internet Gateway. We will likely need x86 machines to serve as exit for many Clients.

The above model that meshes based on low-power radios running in Mesh Point can mesh a small geographic area, such as within the same building with little walls in between. If we need to mesh across buildings over hundreds or thousands of metres, we will need high-power directional line-of-sight links. Two nodes responsible for bridging geographically distant local meshes may look like this:

```
+-------------------+               +-------------------+
|                   | Line-of-sight |                   |
| Ubiquiti LiteBeam | over 5 GHz AC | Ubiquiti LiteBeam |
|                   |<------------->|                   |
+---------+---------+               +---------+---------+
          |                                   |
 Ethernet |                          Ethernet |
          |                                   |
     +----+---------+                    +----+---------+
     |              |                    |              |
     | Raspberry Pi |                    | Raspberry Pi |
     |              |                    |              |
     +--------------+                    +--------------+
```

In the case of a Mesh Point-connected local mesh, peering is automatic over Layer 2. In this case, the ethernet frames between the pair of Ubiquiti LiteBeams are not automatically exposed to the two local Raspberry Pi meshes, unless we explicitly bridge network interfaces. It may however be impractical to extend Layer 2 broadcast domains across the entire city, so we should instead connect the local meshes over IP at Layer 3, the same way we set up cjdns peers over the Internet with the **UDPInterface**.

We can have these bridging Raspberry Pi's generate unique IPv6 addresses, similar to how we generate cjdns addresses, assign them to the ethernet network device, and manually peer with the Raspberry Pi at the other end through these IPv6 addresses. Note that these differ from the cjdns IPv6 identity, which is assigned to the TUN device.

`Validate`: With the above IP peering scheme, verify that the bridging Raspberry Pi's can connect to each other, and that other devices in each local mesh can address devices across the line-of-sight link.

## Links

[cjdns](https://github.com/cjdelisle/cjdns)

[Elvisp](https://github.com/willeponken/elvisp)
