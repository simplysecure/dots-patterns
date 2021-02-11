---
title: Persistent Identity
tags:
  - pattern
  - protocol
  - identity
layout: pattern
---

## The Design Problem

A good design practice is to display extra information that can be used to
locate a particular user. For example, for a federated service like e-mail, you
add the service provider's name in addition to the name
(sally@emailspace.net). This is sufficient but runs into issues when a user
wants to change their name or provider. The user then needs to take on the
cumbersome task of notifying all contacts of their new address. Recipients
would need to trust your new e-mail address, without any strong proof that the
sender is the same person or even using the same device. Users thus rarely
change names or move providers even if they grow to dislike their current
provider.

## The Design Solution

Generate a new `id` when a user creates a profile. This is a sufficiently long
string of characters that would be nearly impossible to guess (e.g., a public
key). If the user changes their service provider or
name, the `id` does not change, allowing an application to keep an
up-to-date contact list and make it easier for users to understand if they are
talking to the same person.

### Examples

PGP (+Keybase)

Various P2P Social Profile Systems (Cabal, SSB, Textile, 3box)

Matrix (p2p beta)

## Why Choose Persistent Identity?

- When you want to enable users to securely move between providers and names
  with ease.

## Best Practice: How to Implement Persistent Identity

- Users need to have strict control over when and where their id is shared.
  Never automatically share this id on a public service
  unless users explicitly opt-in to publicly sharing this id, as it could be used
  nefariously by 3rd parties to contact a user without their consent.
- Make sure that the same id is not reused across names that are intended
  to be separate (e.g., two users on the same device should have two different
  ids).

## Potential Problems with Persistent Identity

By assigning an id to a particular account, it can make it more difficult to
create entirely anonymous accounts. For example, if a 3rd-party finds the id
secret in the profile on the device's hard drive, they have linked that device
to that account. To give extra security guarantees, ensure any identifiers are deleted
completely from devices upon account deletion. See
[disposable-identity](disposable-identity.md) for more information about
anonymous, one-time, and short-lived accounts.

## The Take Away

Persistent identities can help give users continuity and trust in who they're
talking to. It also encourges healthy competition between clients that
implement the protocol, as it's more difficult to lock users into
a specific provider.

## References & Where to Learn More

- PGP local device storage/contact list
- Keybase proofs
- Research papers
