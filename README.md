# Service Desk Simulator Practice

A log of help desk tickets I work through on [servicedesk-simulator.com](https://servicedesk-simulator.com/), written up the way I'd document them on a real service desk.

**Everything in this repo is a simulated environment.** The users, workstations, directory, VPN, and chat are all part of the simulator. This is practice, not production IT experience.

## Why I'm doing this

I'm an Information Technology student at Towson University working toward an entry-level help desk / IT support role. The simulator lets me practice triage, troubleshooting, user communication, and documentation. I write each ticket up in my own words, including what I checked, what worked, and what I'd do differently.

## Entries

| # | Ticket | Issue | Root cause | Link |
|---|--------|-------|------------|------|
| 01 | INC0012847 | Remote user can't reach the Marketing shared drive | VPN was disconnected | [Entry 01](entries/01-marketing-shared-drive-vpn.md) |
| 02 | INC0012871 | Customer Support PC completely dead, agent can't take calls | Not diagnosed. Replaced the desktop instead | [Entry 02](entries/02-dead-desktop-replacement.md) |

More entries get added as I finish and write them up.

## Format of each entry

Every entry follows the same flow, and the sections shift a little depending on the ticket:

1. What the user reported
2. What I checked or decided, in order, with screenshots
3. Root cause (or what was still unknown)
4. Resolution
5. How I confirmed it was fixed
6. Knowledge base notes
7. What I learned
8. Limitations

## Skills practiced so far

- Ticket triage and reading user-reported symptoms
- Directory lookups (profile, group membership, account status)
- Remote desktop troubleshooting
- VPN and remote-access troubleshooting
- Verifying a fix and confirming with the user before closing
- Writing knowledge base notes and escalation notes
- Looking up equipment in an asset management tool
- Reading internal documentation to choose a deployment method
- Imaging a replacement workstation (Server Imaging, PXE boot) and shipping it with a return label
- Prioritizing getting a blocked user working again, and noting what is still undiagnosed

## Notes

- Screenshots come from my own simulator sessions, with identifying details of mine hidden.
- The simulator shows its own solution after a ticket closes. I compare my approach to it, but I write the entries in my own words.
