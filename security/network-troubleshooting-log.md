# Network troubleshooting log -- SCS4.1

Date: 2026-11-25
Station: Station 2

The fair copy of the paper log.  The kit station is the SA team's isolated lab network, never the campus.
Nothing private here: no passwords, no public addresses, no client's name.
The rules: the guess before the first swap.  Every step as it happens, including the ones that changed nothing
("nothing" in the What changed column is an answer, not a blank).  Put it back.  The SA initials the paper log
only after the put-back is checked.

## Fault 1 -- station fault

Symptom (the owner's words): The desk laptop has no internet at all, though phones on the Wi-Fi are working fine.
My guess (device, cable or network): cable
The rung I expected to fail: 1

| Step | What I did (one swap or one look) | What changed | Rung |
|---|---|---|---|
| 1 | Checked RJ45 link lights on the lab laptop and switch port | No link light on either end | 1 |
| 2 | Ran ipconfig /all in PowerShell | Showed Media disconnected and no IPv4 address | 2 |
| 3 | Checked power LED on the switch | nothing | 1 |
| 4 | Traced patch cable behind desk and reseated it into switch LAN port | Steady green link light came on at both ends | 1 |
| 5 | Ran net-look on the laptop | Valid DHCP IP returned and rungs 2 to 5 passed | 2 |
| 6 |  |  |  |

The rung that failed: 1
The fault was: Patch cable unplugged at the switch end behind the desk.
Fixed by: Reseating the Ethernet patch cable firmly into the switch LAN port.
Put back: Yes, cable seated cleanly and station verified by SA.
SA initialled the paper log (yes / not yet): yes

## Fault 2 -- station fault

Symptom (the owner's words): This laptop says Unidentified network and has no internet even though the cable light is on.
My guess (device, cable or network): network
The rung I expected to fail: 2

| Step | What I did (one swap or one look) | What changed | Rung |
|---|---|---|---|
| 1 | Checked link lights on the laptop and router port | nothing | 1 |
| 2 | Ran ipconfig /all in PowerShell | Showed 169.254.x.x APIPA address and blank Default Gateway | 2 |
| 3 | Pinged the station gateway IP | Transmit failed | 3 |
| 4 | Traced cable to back of router and moved it from blue WAN port to yellow LAN port | Link light came up on LAN port | 1 |
| 5 | Ran ipconfig /all and net-look | Valid DHCP IP, gateway, and rungs 2 to 5 passed | 2 |
| 6 |  |  |  |

The rung that failed: 2
The fault was: Desk patch cable moved into the router WAN port instead of a LAN port.
Fixed by: Moving the cable back to a router LAN port so DHCP could assign an address.
Put back: Yes, cable restored to LAN port and checked by SA.
SA initialled the paper log (yes / not yet): yes

## Fault 3 -- fault card, I was the fixer

Sealed log fingerprint (the 12 characters in my break.sh guess file): [b51c88b39e1c]
Card number (after the reveal): 28
Symptom (the owner's words, as my partner said it): The lab laptop connects to Wi-Fi and reaches the router, but cannot open any website by name.
My guess (device, cable or network): device
The rung I expected to fail: 5
My break.sh guess in one line (written before the reveal): The lab device has a manual static DNS server set instead of automatic DHCP DNS because gateway and 8.8.8.8 reply while nslookup times out.

| Step | What I did (one swap or one look) | What changed | Rung |
|---|---|---|---|
| 1 | Checked Wi-Fi connection status in Windows | nothing | 1 |
| 2 | Ran ipconfig /all on the lab laptop | Valid IP and gateway, but DNS server was set to a dead static IP | 2 |
| 3 | Pinged the gateway and 8.8.8.8 | Both replied normally | 4 |
| 4 | Ran nslookup learninglions.org | DNS request timed out | 5 |
| 5 | Wrote guess via break.sh --guess, then reset Wi-Fi IPv4 DNS to Automatic (DHCP) | nslookup resolved learninglions.org immediately | 5 |
| 6 |  |  |  |

The rung that failed: 5
The fault was: Manual invalid DNS server configured on the lab laptop Wi-Fi adapter.
Fixed by: Setting IPv4 DNS assignment back to Automatic (DHCP) on the lab device.
Proved on the lab device with the ladder (the rungs that passed after the fix): Rungs 1, 2, 3, 4, and 5 all passed (ipconfig /all, ping gateway, ping 8.8.8.8, and nslookup learninglions.org).
Put back (the undo line break.sh printed, done by hand and checked): Reset Wi-Fi adapter DNS to Automatic (DHCP) and verified with ipconfig /all.
SA initialled the paper log (yes / not yet): yes
Was my guess right, and what did the reveal add: Yes, my guess was right that DNS was overridden on the device; the reveal confirmed Card 29 set a dead static DNS address.

## The card I planted -- I was the partner

Card number: 27
The step break.sh printed, done by hand on the lab device (in my words, no passwords): Set a manual static IPv4 address outside the station subnet on the lab laptop Wi-Fi adapter with SA admin approval and closed the Ubuntu-SCS tab.
The undo, done by hand after the fixer finished, and how we checked it: Switched Wi-Fi IPv4 back to Automatic (DHCP) by hand, ran ipconfig /all and net-look to confirm valid station IP and gateway, and had the SA initial.
The first thing my partner's log got right: Wrote their one-word guess (network) and expected rung (2) before touching the keyboard.
