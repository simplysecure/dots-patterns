---
title: trackers
category: sync-status
tags:
  - pattern
  - protocol
  - p2p
  - infrastructure
description: "Trackers can facilitate introduction in peer-to-peer networks."
layout: pattern
---

## The Design Problem

On centralized social networks, users can identify content and peers relevant to their own interests and "follow" or "subscribe" to the content. The platform provides the supporting infrastructure to connect with peers and browse available content.

This is not always true in peer-to-peer systems. Once a user found peers offering relevant content, they can ask those peers for contact information for adjacent peers, and connect to a larger portion of the network - but finding the initial "introduction" peers is a complicated challenge.

(Even once relevant peers are identified, creating a peer-to-peer network connection between two home networks requires NAT traversal, also referred to as NAT hole punching. This usually involves utilizing a third party to exchange network address and port information to facilitate a direct connection.)

## The Design Solution

Create centralized "tracker" servers to introduce peers. These trackers have well known addresses (e.g., HTTP or IP addresses) so they can be easily found by users, and may even have their addresses included in client software to aid peer discovery.

Trackers are a database of content that is available and the contact information for devices that have that content. Traditionally, this contact information is in the form of an IP address and port number, and may contain additional metadata about the peer's bandwidth and supported functionality. However, the contact information could take a variety of other forms, including onion addresses, public keys, or other related content.

### Examples

Trackers are famously used by torrents to introduce peers to content seeds. They are also used to add new peers to distributed hash tables, or similar communication networks like blockchains. Examples include:

- Torrents
- Kademlia DHT
- Blockchains
- Tor Directory Servers
- IPFS Bootstrap Peers
- Cabal

## Why Choose Trackers?

Trackers are a simple technique to solve "first introduction" problems in peer-to-peer systems, provide a natural solution to NAT traversal, and can serve as a bootstrapping step to add clients to a more decentralized network like a distributed hash table.

## Best Practice: How to Implement Trackers

- Include multiple redundant trackers in content links (such as torrent files or magnet links) or hardcoded in client software
- Have clients periodically re-submit their contact information to trackers to indicate continual interest in content
- Trackers may prune contact information after an age threshold, or their may include the last "check-in date" with any contact information to allow clients to make pruning decisions on their own

## Potential Problems with Trackers

- Centralized trackers make surveillance easier and introduce a small number of critical hubs that can be disrupted to prevent new clients from joining a network
- By default, trackers can read any contact information supplied to them, and so can identify the number of peers interested in an identifier and their contact information
- Mitigate this vulnerability by encrypting the contact information before submitting it to a tracker, and using a derived hash of the encryption key as a tracker identifier, so interested peers will be able to read the peer contact data
- Trackers only solve discovery of peers based on a shared content, but do _not_ necessarily facilitate discovery of new content.
- Content identifiers must be shared beforehand, so trackers do not completely solve content discovery.

## The Take Away

Trackers are a common component of many peer-to-peer networks, and facilitate peer introduction.

## **References & Where to Learn More**
