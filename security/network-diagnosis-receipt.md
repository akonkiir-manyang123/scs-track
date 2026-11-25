# AI diagnosis receipt -- SCS4.1

One prompt, before the hands touch the kit, inside the five moves.  Nothing private in it: no router password,
no client's name, no public address, no screenshot.  The hands follow the ladder, not the tool.

Tool (and tier): Gemini (web)
Date: 2026-11-25
The fault it was for (Fault 1, 2 or 3 in the log): Fault 1
The prompt, word for word: A wired office laptop has no internet connection while smartphones on the same office Wi-Fi are browsing normally. What would you check first, and in what order?
Its order of checks (one line): 1. Restart the router and modem; 2. Run ipconfig /all to check IP and DNS; 3. Flush DNS and reset Winsock; 4. Check the Ethernet cable and switch port.
Where it matched the ladder: Matched Rung 2 (ipconfig /all) and Rung 5 (DNS).
The rung it skipped or invented: Skipped Rung 1 (physical link lights and cable seating) at the start and invented restarting the router first.
What my hands did instead, and why: Checked Rung 1 link lights and the patch cable at the switch first because working Wi-Fi phones already proved the router was online, and rebooting would disrupt users.
Label: AI-assisted diagnosis, checked against the ladder
