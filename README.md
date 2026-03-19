Unsocial
unsocial6136
Online





Text Channel
Chestlock Official:admin-chat
Search Chestlock Official

admin-chat chat
Welcome to #admin-chat!
This is the start of the #admin-chat channel. 

Edit Channel
January 4, 2026

Unsocial — 1/4/2026 3:42 PMSunday, January 4, 2026 3:42 PM

[3:44 PM]Sunday, January 4, 2026 3:44 PM
Identify hot path. Locate listener for InventoryMoveItemEvent (hopper transfers). Confirm it runs sync and fires for every hopper move. Add temporary timing counters (nanoTime) around your hopper handler and around lock and group lookups to confirm cost.

Add immediate config kill-switch. Add config options hopper-protection true/false, hopper-minecart-protection true/false, hopper-cache-ttl-ticks 0–200 default 20. In InventoryMoveItemEvent handler, if hopper-protection is false return. If holder is minecart and hopper-minecart-protection is false return.

Stop scanning YAML on each hopper move (core fix). Create a BlockKey type with fields UUID worldId and int x y z with equals and hashCode. In LockController add in-memory indexes Map<BlockKey, LockEntry> locksByBlock and optionally Map<String, Set<String>> sharedMembersByOwner. Define LockEntry with owner, isPublic, allowedPlayers as a Set, and optional allowHoppers. On plugin enable build indexes from disk once by loading locks.yml, iterating the locks section a single time, and filling locksByBlock. Do not rely on retrieveSubSections or full scans for lookups anymore.

Expand (21 lines)
message.txt
message.txt (5 KB)
5 KB
Change language
View whole file
More
January 5, 2026

Unsocial — 1/5/2026 8:21 AMMonday, January 5, 2026 8:21 AM

[8:21 AM]Monday, January 5, 2026 8:21 AM
i cant believe that fixed it first try

id3nt1ty — 1/5/2026 1:31 PMMonday, January 5, 2026 1:31 PM
You are so popular

Unsocial — 1/5/2026 1:31 PMMonday, January 5, 2026 1:31 PM
fr
[1:31 PM]Monday, January 5, 2026 1:31 PM
disco when

id3nt1ty — 1/5/2026 1:32 PMMonday, January 5, 2026 1:32 PM
30 min

Unsocial — 1/5/2026 1:32 PMMonday, January 5, 2026 1:32 PM

:heart:
Click to react
:thumbsup:
Click to react
:fire:
Click to react
Add Reaction
Edit
Forward
More
March 19, 2026

Unsocial — 2:03 PMThursday, March 19, 2026 2:03 PM
# ChestLock

ChestLock is a Spigot storage-protection plugin for Minecraft 1.21 servers. It lets players lock supported containers, share access with other players, organize shared access through groups, and block unauthorized hopper automation into protected inventories.

This README describes the current source tree in this repository. The plugin metadata currently reports version `1.5.5`, API version `1.21`, and main class `com.watsonllc.chestlock.Main`.

## Overview

ChestLock is built around a simple interaction model:

1. Players place or claim a supported block.
2. ChestLock creates or manages a lock entry for that block.
3. Access checks run when players interact with the block.
4. Hopper checks run when automated item transfers involve protected inventories.

The plugin is intentionally configuration-driven. Lockable block types, permissions, hopper behavior, messages, sorting, update checks, and explosion protection are all controlled through `config.yml`.

## Feature Summary

### Core protection

- Auto-locks supported blocks on placement when `settings.autoLock` is enabled.
- Supports explicit claiming of unlocked blocks with `/chestlock claim`.
- Stores one or more allowed players per lock.
- Lets owners toggle locks between private and public.
- Prevents players from opening or breaking locks they do not own unless they are bypassing.

### Sharing and collaboration

- Supports direct sharing with `/chestlock add <player>` and `/chestlock remove <player>`.
- Supports group-based sharing through `/chestlock group ...`.
- Treats players in the same ChestLock group as trusted for access checks.

### Hopper protection

- Tags placed hoppers with the player who placed them.
- Tags placed hopper minecarts shortly after placement.
- Can deny or allow transfers based on source ownership, destination ownership, and the configured untagged-hopper policy.
- Includes an admin maintenance command to tag old hoppers in loaded chunks.

### Quality-of-life and admin features

- Optional intrusion alerts per lock.
- Shift-click debug output for lock metadata.
- Optional chest/player inventory sorting.
- Optional explosion resistance for lockable blocks.
- Update check on startup and join for players with the appropriate permission.
- Config version guard that disables normal behavior when an incompatible config is detected.

## Compatibility and Requirements

| Item | Value |
| --- | --- |
| Server API | Spigot API `1.21` |
| Java target | Java `17` |
| Command root | `/chestlock` |
| Main class | `com.watsonllc.chestlock.Main` |
| Project style | Eclipse Java project |
| Build tool | None included in this repo |

The Eclipse classpath in this repository points at a local Spigot API `1.21.11-R0.2-SNAPSHOT` jar. For practical use, treat the plugin as a Java 17 Spigot/Paper 1.21.x plugin.

## Installation

1. Build or obtain the ChestLock jar.
2. Copy the jar into your server's `plugins/` directory.
3. Start the server once so ChestLock can generate its data folder and default files.
4. Review `plugins/ChestLock/config.yml`.
5. Grant permissions through your permission plugin, or disable `settings.usePermissions` if you do not use one.
6. Restart or reload the server after making configuration changes.

### First-run files

ChestLock creates and uses these files under `plugins/ChestLock/`:

- `config.yml`: runtime settings, messages, lockables, and action labels.
- `locks.yml`: lock storage.
- `groups.yml`: group membership and invite storage.

## Quick Start for Players

### Locking a block

With default settings, players usually do not need a command to create a lock:

1. Place a supported container or block.
2. Wait a brief moment for the delayed auto-lock task to run.
3. The block becomes owned by the placing player.

To claim an existing unlocked block:

1. Run `/chestlock claim`
2. Right-click the target block.

### Sharing a lock

1. Run `/chestlock add <player>`
2. Right-click the protected block you own.

To remove access:
... (287 lines left)

Collapse (387 lines)
README.md
README.md (17 KB)
17 KB
Change language
View whole file
More
:heart:
Click to react
:thumbsup:
Click to react
:fire:
Click to react
Add Reaction
Edit
Forward
More

Message #admin-chat
﻿
Upgrade your friends! Gift them awesome chat perks with Nitro.
Send GIF
Members list for admin-chat (channel)
Developer, 1 member
Developer
 — 1

Unsocial
Bot, 1 member
Bot
 — 1

Carl-bot
VERIFIED APP
APP
/help | carl.gg
/help | carl.gg
# ChestLock

ChestLock is a Spigot storage-protection plugin for Minecraft 1.21 servers. It lets players lock supported containers, share access with other players, organize shared access through groups, and block unauthorized hopper automation into protected inventories.

This README describes the current source tree in this repository. The plugin metadata currently reports version `1.5.5`, API version `1.21`, and main class `com.watsonllc.chestlock.Main`.

## Overview

ChestLock is built around a simple interaction model:

1. Players place or claim a supported block.
2. ChestLock creates or manages a lock entry for that block.
3. Access checks run when players interact with the block.
4. Hopper checks run when automated item transfers involve protected inventories.

The plugin is intentionally configuration-driven. Lockable block types, permissions, hopper behavior, messages, sorting, update checks, and explosion protection are all controlled through `config.yml`.

## Feature Summary

### Core protection

- Auto-locks supported blocks on placement when `settings.autoLock` is enabled.
- Supports explicit claiming of unlocked blocks with `/chestlock claim`.
- Stores one or more allowed players per lock.
- Lets owners toggle locks between private and public.
- Prevents players from opening or breaking locks they do not own unless they are bypassing.

### Sharing and collaboration

- Supports direct sharing with `/chestlock add <player>` and `/chestlock remove <player>`.
- Supports group-based sharing through `/chestlock group ...`.
- Treats players in the same ChestLock group as trusted for access checks.

### Hopper protection

- Tags placed hoppers with the player who placed them.
- Tags placed hopper minecarts shortly after placement.
- Can deny or allow transfers based on source ownership, destination ownership, and the configured untagged-hopper policy.
- Includes an admin maintenance command to tag old hoppers in loaded chunks.

### Quality-of-life and admin features

- Optional intrusion alerts per lock.
- Shift-click debug output for lock metadata.
- Optional chest/player inventory sorting.
- Optional explosion resistance for lockable blocks.
- Update check on startup and join for players with the appropriate permission.
- Config version guard that disables normal behavior when an incompatible config is detected.

## Compatibility and Requirements

| Item | Value |
| --- | --- |
| Server API | Spigot API `1.21` |
| Java target | Java `17` |
| Command root | `/chestlock` |
| Main class | `com.watsonllc.chestlock.Main` |
| Project style | Eclipse Java project |
| Build tool | None included in this repo |

The Eclipse classpath in this repository points at a local Spigot API `1.21.11-R0.2-SNAPSHOT` jar. For practical use, treat the plugin as a Java 17 Spigot/Paper 1.21.x plugin.

## Installation

1. Build or obtain the ChestLock jar.
2. Copy the jar into your server's `plugins/` directory.
3. Start the server once so ChestLock can generate its data folder and default files.
4. Review `plugins/ChestLock/config.yml`.
5. Grant permissions through your permission plugin, or disable `settings.usePermissions` if you do not use one.
6. Restart or reload the server after making configuration changes.

### First-run files

ChestLock creates and uses these files under `plugins/ChestLock/`:

- `config.yml`: runtime settings, messages, lockables, and action labels.
- `locks.yml`: lock storage.
- `groups.yml`: group membership and invite storage.

## Quick Start for Players

### Locking a block

With default settings, players usually do not need a command to create a lock:

1. Place a supported container or block.
2. Wait a brief moment for the delayed auto-lock task to run.
3. The block becomes owned by the placing player.

To claim an existing unlocked block:

1. Run `/chestlock claim`
2. Right-click the target block.

### Sharing a lock

1. Run `/chestlock add <player>`
2. Right-click the protected block you own.

To remove access:

1. Run `/chestlock remove <player>`
2. Right-click the protected block.

### Making a lock public

1. Run `/chestlock public`
2. Right-click the lock you own.

Run the same command again and right-click the lock to switch it back to private.

### Toggle mode

The following commands support `toggle` mode:

- `/chestlock add <player> toggle`
- `/chestlock remove <player> toggle`
- `/chestlock claim toggle`
- `/chestlock destroy toggle`
- `/chestlock public toggle`

Toggle mode keeps the action armed until it is manually canceled or times out. The timeout is currently 15 seconds.

## Commands

All commands use `/chestlock` as the root command.

| Command | Permission | Description |
| --- | --- | --- |
| `/chestlock` | none | Shows the help menu filtered by available permissions. |
| `/chestlock add <player> [toggle]` | `chestlock.add` | Arms the next right-click to add a shared owner. |
| `/chestlock remove <player> [toggle]` | `chestlock.remove` | Arms the next right-click to remove a shared owner. |
| `/chestlock claim [toggle]` | `chestlock.claim` | Claims an unlocked supported block. |
| `/chestlock destroy [toggle]` | `chestlock.destroy` | Removes a lock from a protected block. |
| `/chestlock public [toggle]` | `chestlock.public` | Toggles a lock between public and private. |
| `/chestlock bypass` | `chestlock.bypass` | Toggles bypass mode for admin use. |
| `/chestlock group create <group>` | `chestlock.group.create` | Creates a group and makes the sender the owner. |
| `/chestlock group delete` | `chestlock.group.delete` | Deletes the group owned by the sender. |
| `/chestlock group invite <player>` | `chestlock.group.invite` | Invites a player to the sender's group. |
| `/chestlock group add <player>` | `chestlock.group.invite` | Alias of `group invite`. |
| `/chestlock group remove <player>` | `chestlock.group.remove` | Removes a player from the sender's group. |
| `/chestlock group accept [group]` | `chestlock.group.accept` | Accepts a pending invite. |
| `/chestlock group decline [group]` | `chestlock.group.decline` | Declines a pending invite. |
| `/chestlock group invites` | `chestlock.group.invites` | Lists pending group invites. |
| `/chestlock group leave` | `chestlock.group.leave` | Leaves the current group. If the owner leaves, the group is deleted. |
| `/chestlock group list` | `chestlock.group.list` | Lists members of the current group. |
| `/chestlock taghoppers <owner> <radius-or-world> [minecarts]` | `chestlock.taghoppers` | Tags unowned hoppers in loaded chunks for hopper-protection migration and cleanup. |

### `taghoppers` behavior

- If the second argument is a number, ChestLock treats it as a radius around the command sender and only works when the sender is a player.
- If the second argument is a world name, ChestLock scans loaded chunks in that world.
- `minecarts` includes hopper minecarts in the pass.
- Existing hopper owner tags are preserved.
- The command only processes loaded chunks.

## Permissions

Most player command permissions are only enforced when `settings.usePermissions` is `true`.

| Permission | Purpose |
| --- | --- |
| `chestlock.add` | Use `/chestlock add` |
| `chestlock.remove` | Use `/chestlock remove` |
| `chestlock.claim` | Use `/chestlock claim` |
| `chestlock.destroy` | Use `/chestlock destroy` |
| `chestlock.public` | Use `/chestlock public` |
| `chestlock.bypass` | Toggle bypass mode |
| `chestlock.updatechecker` | Receive update notifications on join |
| `chestlock.taghoppers` | Use `/chestlock taghoppers` |
| `chestlock.group.create` | Create groups |
| `chestlock.group.delete` | Delete owned groups |
| `chestlock.group.invite` | Invite players to a group |
| `chestlock.group.remove` | Remove players from a group |
| `chestlock.group.accept` | Accept group invites |
| `chestlock.group.decline` | Decline group invites |
| `chestlock.group.invites` | View pending invites |
| `chestlock.group.leave` | Leave a group |
| `chestlock.group.list` | List group members |

### Permission note

The repository also contains a legacy `permissions` helper file. The authoritative permission checks are the nodes used in the Java source and listed above.

The current code also hard-checks `chestlock.bypass`, `chestlock.taghoppers`, and `chestlock.updatechecker` directly, even if `settings.usePermissions` is disabled.

Legacy nodes such as `chestlock.bypass.*` and `chestlock.group.add` appear in helper files, but they are not the permission checks used by the current command handlers.

## Supported Lockables

### Enabled by default

- Anvils
- Barrels
- Blast furnaces
- Chests
- Copper chest variants
- Dispensers
- Droppers
- Enchanting tables
- Furnaces
- Hoppers
- Jukeboxes
- Smokers
- Trapped chests

### Disabled by default

- Ender chests
- All shulker box colors
- All configured door types

### Double chest behavior

Double chests are handled by iterating both connected chest halves. In practice this means:

- Auto-locking protects both halves.
- Destroy/claim flows operate across both halves.
- Breaking one half can move the remaining lock entry to the surviving half when needed.

## Configuration Reference

The default config is stored at [`src/config.yml`](src/config.yml) in this repository and becomes `plugins/ChestLock/config.yml` at runtime.

### Core settings

| Path | Default | Meaning |
| --- | --- | --- |
| `settings.usePermissions` | `true` | Enforces permission checks on commands. |
| `settings.updateChecker` | `true` | Checks for updates on startup and player join. |
| `settings.prefix` | `&8[&6ChestLock&8] &7` | Prefix added to `messages.*`. |
| `settings.autoLock` | `true` | Automatically creates locks for placed supported blocks. |
| `settings.tntProof` | `true` | Removes lockable blocks from explosion block lists. |
| `settings.hopper-protection` | `true` | Enables hopper transfer enforcement. |
| `settings.hopper-minecart-protection` | `true` | Includes hopper minecarts in hopper enforcement. |
| `settings.hopper-check-source` | `true` | Evaluates source inventory ownership. |
| `settings.hopper-check-destination` | `true` | Evaluates destination inventory ownership. |
| `settings.hopper-cache-ttl-ticks` | `20` | Cache TTL for hopper decisions. `0` disables the cache. |
| `settings.untagged-hoppers` | `ALLOW` | Policy for legacy hoppers without owner tags: `ALLOW`, `DENY`, or `TAG_ON_USE`. |
| `settings.sortInventoryEnabled` | `false` | Enables inventory sorting hooks. |
| `settings.sortBy` | `type` | Sort mode: `type` or `alphabetical`. |
| `settings.sortWith` | `DOUBLE_CLICK` | Click type that triggers sorting. |
| `settings.intrusionAlerts` | `true` | Enables alert support for protected locks. |
| `settings.alertRadius` | `15` | Radius used to suppress alerts when an owner is already nearby. |
| `settings.lockID-characters` | alphanumeric | Character set for generated lock IDs. |
| `settings.lockID-size` | `12` | Length of generated lock IDs. |
| `configVersion` | `1.4.1` | Internal guard used to detect incompatible configs. |

### Lockables and doors

- `lockables.*` enables or disables container-like block families.
- `lockables-doors.*` enables or disables door locking support.
- `messages.*` customizes all user-facing messages.
- `actions.*` customizes the labels used in timeout and cancellation messages.

### Important config caveat

The config contains a `lockables.COPPER_CHEST` entry, but the current `Utils.lockableBlock` implementation reads `lockables.CHEST` for standard and copper chest variants. If you want to disable chest locking in the current codebase, the effective toggle is `lockables.CHEST`.

## Lock and Group Data

### `locks.yml`

Locks are stored under `Locks.<lockId>`. A lock record includes:

- `public`
- `allowed`
- `type`
- `intrusionAlert`
- `location.world`
- `location.x`
- `location.y`
- `location.z`

The first entry in `allowed` is treated as the owner. Additional entries are treated as directly shared owners.

### `groups.yml`

Groups are stored under `Groups.<groupName>`. A group record includes:

- `owner`
- `members`
- `invites`

Group names are normalized to lowercase in storage and in-memory indexes.

## Runtime Behavior Details

### Access checks

- If a block is not locked, ChestLock does nothing.
- If a lock is public, interaction is allowed.
- If a player is listed in `allowed`, interaction is allowed.
- If the player shares a ChestLock group with the owner, interaction is allowed.
- Otherwise the interaction is canceled and the player is told who owns the lock.

### Placement rules

- ChestLock blocks placement of a supported lockable adjacent to someone else's protected lock.
- This restriction is skipped for bypassing players.
- Hoppers are tagged with the placing player's name at placement time.

### Break behavior

- Owners can break their own protected blocks and the lock entry is removed.
- For double chests, ChestLock attempts to preserve protection on the remaining half when appropriate.
- Non-owners cannot break protected lockable blocks unless bypass mode is enabled.

### Bypass mode

Bypass mode is intended for administrative work:

- It skips access restrictions.
- It skips adjacency placement restrictions.
- It suppresses auto-lock creation.
- The plugin warns the player once when bypass mode prevents a lock from being created.

### Intrusion alerts

Owners can toggle intrusion alerts by sneaking and left-clicking a protected block while holding redstone. When enabled, unauthorized open attempts trigger a message to online owners if they are outside the configured alert radius.

### Debug action

Players can inspect a lock by sneaking and left-clicking it with an empty main hand. ChestLock prints:

- Lock ID
- Lock type
- Public state
- Owner list

## Project Structure

The codebase is organized by responsibility rather than by large, multi-purpose classes.

| Path | Responsibility |
| --- | --- |
| `src/com/watsonllc/chestlock/Main.java` | Plugin bootstrap and startup orchestration |
| `src/com/watsonllc/chestlock/commands/` | Root command dispatcher and tab completion |
| `src/com/watsonllc/chestlock/commands/admin/` | Admin commands such as bypass and hopper tagging |
| `src/com/watsonllc/chestlock/commands/player/` | Player-facing action commands |
| `src/com/watsonllc/chestlock/events/` | Bukkit listeners and event wiring |
| `src/com/watsonllc/chestlock/logic/` | Domain logic, lock/group models, hopper decisions, player state |
| `src/com/watsonllc/chestlock/config/` | Config and YAML-backed persistence wrappers |

### Important classes

- `LockController`: central in-memory lock index and lock persistence adapter.
- `GroupController`: group membership, invite handling, and shared-access resolution.
- `PlayerStateManager`: tracks temporary command actions and bypass state.
- `InventoryMove`: hopper protection pipeline.
- `HopperDecisionSimulator`: isolated hopper decision engine.
- `HopperCache`: short-lived cache for repeated hopper transfer decisions.

## Building From Source

This repository does not include Maven or Gradle configuration. The project is currently structured for direct IDE compilation.

### Recommended approach

1. Import the repository as an existing Eclipse Java project.
2. Add a Spigot/Paper API jar for Minecraft 1.21.x if your environment does not already match the `.classpath`.
3. Compile the Java sources to `bin/`.
4. Package the compiled classes together with:
   - `plugin.yml` at the jar root
   - `config.yml` at the jar root
5. Drop the resulting jar into the server's `plugins/` folder.

### Testing note

There is no formal automated test suite in this repository. `HopperDecisionSimulatorTest` is a small standalone Java entry point used to validate hopper decision rules outside the server runtime.

## Troubleshooting

| Problem | Likely cause | What to check |
| --- | --- | --- |
| Commands say you lack permission | Permission enforcement is enabled | Grant the node or set `settings.usePermissions: false` |
| Locks stop working after an update | Config version mismatch | Delete `plugins/ChestLock/config.yml` and let the plugin regenerate it |
| A newly placed container does not lock | Auto-lock disabled or bypass mode enabled | Check `settings.autoLock` and whether the player is bypassing |
| Hopper protection blocks legacy hoppers | Old hoppers may be untagged | Run `taghoppers` or review `settings.untagged-hoppers` |
| Group invite commands behave unexpectedly | Target is already in a group or invite lookup is ambiguous | Check current membership and pending invites |

## Notes for Maintainers

- The current source is more trustworthy than the legacy helper files in the repo root.
- The readme intentionally documents current implementation behavior, including quirks such as copper chests following the `CHEST` toggle.
- If you add or rename commands, permissions, or config keys, update this file at the same time to keep server-admin documentation aligned with the code.
