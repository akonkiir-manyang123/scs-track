# Method note -- SCS4.1

## 1. What I set out to do
Map a small office network, read Windows and Ubuntu-SCS IP layers, isolate two station faults and a fault card from Rung 1, harden the station router, reserve the printer IP, and map a real shop.

## 2. What I did, in order
Installed the SCS4.1 tools, drew the six-box office map, read Windows/WSL/phone addresses with ipconfig and net-look, found the bad cable by swapping, isolated Faults 1 and 2 plus Card 29 from Rung 1, hardened the station router, reserved the printer IP, and mapped a local shop.

## 3. How I checked it worked
Verified rungs 2 to 5 passed on net-look after every fix and router restart, printed test pages from both the lab laptop and phone after reserving the printer IP, and had the SA initial each paper log.

## 4. What went wrong and what I did about it
The AI diagnosis tool suggested rebooting the router first and skipped Rung 1 (Lights), and the printer changed IP after an unreserved reboot; I followed the ladder from Rung 1 instead and added a DHCP reservation on the router.

## 5. What I would do differently next time
Write down the printer's MAC address and reserve its IP in DHCP before adding it to client laptops so restarts never cause Offline errors.

## 6. What I might be wrong about, and how I would find out
I assumed reserving the printer IP on the router guarantees it never changes, but if the router resets to factory defaults after a power surge it could lose the reservation; I would find out during the second-look power-off check by reading the printer's panel address again.
