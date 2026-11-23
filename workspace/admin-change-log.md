# Admin change log -- SCS3.1

Date: 2026-11-17
Sandbox admin sign-in: akon@<sandbox domain>
My unit: /Trainees/akon
Naming convention: first.last

One row per admin action, written BEFORE the click.  A ticket may take several rows; add them as you go.
Logged at: the time on the laptop clock when you wrote the row.
Console path: where you expect to click, with ">" between the steps; correct it after if the console differs.
Audit log: filled in SGL/Lab -- the time the console's audit log shows for this change, or "gap:" and why.
Never write a password here.  The first password is handed over by voice.

| # | Ticket | Logged at | What I am about to change (console path) | Who or what it affects | Why (the three questions, one line) | How I checked it | Audit log |
|---|---|---|---|---|---|---|---|
| 1   | 1 New starter    | 10:50     | Admin console > Directory > Users > Add new user                              | amina.okello, new Front Desk starter                                         | The job needs counter email and calendar, extra access risks financial records, the owner decided             | Verified user appears active in users list and signed in via private window     | 10:52     |
| 2   | 2 Groups         | 10:55     | Admin console > Directory > Groups > Create group                             | counter@<sandbox-domain>, counter staff                                      | Staff need one shared address for shift rotas, wider access exposes management mail, the shop manager decided | Verified group page lists all counter members                                   | 10:57     |
| 3   | 3 Units          | 11:00     | Admin console > Directory > Organizational units > Create organizational unit | Front Desk under /Trainees/akon/Staff                                | Chat must be turned off for counter staff only while other staff keep it, the owner decided                   | Verified Front Desk OU appears in tree and moved new starter into it            | 11:02     |
| 4   | 4 Delegated role | 11:05     | Admin console > Account > Admin roles > Assign users                          | Accountant user in /Trainees/akon/Staff, Password Reset Admin        | The job needs password resets for staff only, full admin risks billing and data deletion, the owner decided   | Signed in as accountant and tested three actions to confirm role limits         | 11:07     |
| 5   | 5 Rollback       | 11:10     | Admin console > Account > Admin roles > Unassign users                        | Accountant user in /Trainees/akon/Staff, remove Password Reset Admin | The role test is complete and elevated privileges are no longer needed, the trainer decided                   | Confirmed Password Reset Admin role is removed from the accountant user profile | 11:12     |


## Gaps

## SCS3.2 -- sharing, security, backups, offboarding (2026-11-18)

Practice OU only.  Every row written before the click; the check column filled after it.

| # | Time | What I am about to change (console path) | Who or what it affects | Why, in one line | How I checked it | Undo |
|---|---|---|---|---|---|---|
| 1 | 09:15 | Admin console > Apps > Google Workspace > Drive and Docs > Sharing settings | Practice OU (/Trainees/akon) external sharing | Restrict outside sharing to prevent accidental data leaks while keeping internal collaboration working | Tested sharing a test file to an external address and confirmed it was blocked | Revert Sharing settings to previous domain default |
| 2 | 09:22 | Admin console > Apps > Google Workspace > Drive and Docs > Manage shared drives | Front Desk Shared Drive for /Trainees/akon | Move team files out of personal My Drive into a business-owned shared drive so files survive staff turnover | Confirmed Front Desk Shared Drive appears and accepts member uploads | Delete empty shared drive or move files back |
| 3 | 09:30 | Admin console > Apps > Google Workspace > Drive and Docs > Shared drive settings | Front Desk Shared Drive link sharing | Set default access to restricted so no business file is left open via link sharing | Checked file sharing dialog and verified General access defaults to Restricted | Re-enable link sharing on the shared drive settings |
| 4 | 09:38 | Admin console > Security > Authentication > 2-Step Verification | Practice OU (/Trainees/akon) sign-in policy | Enforce 2-Step Verification for all practice users to protect accounts against stolen passwords | Signed in with practice user in second browser profile and completed 2-step enrollment | Turn off 2-Step Verification enforcement for /Trainees/akon |
| 5 | 09:46 | Admin console > Devices > Mobile and endpoints > Settings > Universal settings | Practice OU (/Trainees/akon) mobile and endpoint devices | Require screen lock on devices accessing Workspace data so a lost device cannot expose client files | Verified screen lock requirement appears under Practice OU device policy | Disable screen lock enforcement under Universal settings |
| 6 | 09:55 | Admin console > Security > Access and data control > Google Takeout | Practice OU (/Trainees/akon) user data export | Ensure Drive is enabled in Takeout so monthly user backups include Drive files | Verified Drive service toggle is enabled for /Trainees/akon | Disable Google Takeout service for /Trainees/akon |
| 7 | 10:10 | Admin console > Directory > Users > amina.otieno > Suspend user | amina.otieno@<sandbox domain> (leaver offboarding) | Suspend leaver account immediately upon departure without deleting data so audit trail and files remain intact | Confirmed status changed to Suspended and leaver sign-in was refused | Click Reactivate user on amina.otieno profile |
| 8 | 10:20 | Admin console > Apps > Google Workspace > Drive and Docs > Transfer ownership | Drive files from amina.otieno to david.kamau | Transfer leaver's Drive files to manager david.kamau so business records stay accessible | Verified customer-list.csv and price-list.csv now list david.kamau as owner in Drive log | Transfer ownership back to amina.otieno after reactivation |
| 9 | 10:35 | Admin console > Directory > Users > amina.otieno > Reactivate user | amina.otieno@<sandbox domain> (end-of-lab reset) | Un-suspend practice user at the end of SGL/Lab so the practice OU is left whole | Verified user status returned to Active in Users list | Suspend user again if needed |
| 10 | 10:42 | Admin console > Directory > Users > Download users | Practice OU (/Trainees/akon) post-reset export | Export updated users list confirming all practice OU members are active and intact | Checked exported CSV and confirmed zero suspended or missing users | Delete exported CSV from local evidence folder |
