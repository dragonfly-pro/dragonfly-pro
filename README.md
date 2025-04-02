# dragonfly-pro
⚠️ **Warning**: This project is not fully complete.

A Dragonfly fork that adds multi-version support, exposes required APIs, and includes more vanilla features while maintaining compatibility with upstream.

## What is the current problem in original the Dragonfly?
- They don't want to expose an API to access the Minecraft protocol, which is good, but it may limit developers from using packets since Dragonfly's abstraction layer for Minecraft packets is not fully implemented yet.
  - "_but there is reflect_"
    Well, we used that before, but it significantly degraded performance. For example, as you know, accessing a private field of a struct using reflection is ~30-100x slower than direct access.
- We want to merge good PRs that were never merged in Dragonfly.
- Gophertunnel's multi-version API is not sufficient. For example, we can't add support for versions below 1.20.60 because they use a different compression system, which we can't do that in Gophertunnel.

## Goals
(subject to change)
- [ ] Multi Version
- [ ] Entity Rework
- [ ] Entity Link API
  - [ ] Fishing Rod
  - [ ] Entity Riding
- [ ] Optimize performance
  - [ ] Broadcast packets (like PocketMine): encode once, send to multiple recipients.
  - [ ] Packet caching for heavy packets
    - [ ] packet.CraftingData
- [ ] Fix known dragonfly bugs
  - [ ] https://github.com/df-mc/dragonfly/issues/989
  - [ ] https://github.com/df-mc/dragonfly/issues/1003
- [ ] Blocks
  - [ ] Snow Layer
- [ ] Handler
  - [ ] Block Update Handler
    - [ ] neighbour update
    - [ ] random tick update
  - [ ] Packet Handler: There's a library like https://github.com/bedrock-gophers/intercept, but we can't get the caller *world.Tx when handling server packets.
  - [ ] Crafting Handler
  - [ ] Centralized Player Inventory Handler

## How to use
Just add this at the end of the `go.mod` file:
```
replace github.com/df-mc/dragonfly => github.com/dragonfly-pro/dragonfly-pro master
```
After that, run the `go get` command
