# Access map -- the reference shop (an invented business) -- SCS3.1

This is an AI-assisted example access map for an invented business.
It is not a record of permissions applied in a live Admin console.

Groups are people; units are settings; every person is in one unit and many groups.
Why: what the job needs, what goes wrong with more, and who decided.

| Person (job) | What the job needs | OU | Groups | Admin role | Why (one line) |
|---|---|---|---|---|---|
| The owner | All business settings, users and security | /Owners | Shop-Owners | Super Admin | Needs full control of the business; extra access is not appropriate for other staff; the owner decides. |
| The accountant (a sandbox user, ticket 4) | Financial records and billing information | /Staff | Finance | None | Needs financial records for accounting; user and security administration would be unnecessary risk; the owner decides. |
| The shop manager | Staff schedules, stock and shop operations | /Staff | Shop-Managers | None | Needs to coordinate shop work; access to security settings could cause disruption; the owner decides. |
| Counter staff (four) | Sales records and counter information | /Staff/Front Desk | Counter-Team | None | Needs counter tools to serve customers; access to payroll and administration is unnecessary; the owner decides. |
| The new starter (a sandbox user, ticket 1) | Basic front desk tools and training materials | /Staff/Front Desk | Front-Desk, Trainees | None | Needs only starter duties and training; wider access could expose business information; the owner decides. |
| Welders (three) | Workshop schedules and job instructions | /Workshop | Fabrication-Team | None | Needs workshop instructions to complete jobs; financial and user administration access is unnecessary; the owner decides. |
| Drivers (two) | Delivery schedules and dispatch information | /Delivery | Delivery-Team | None | Needs delivery details to complete routes; access to staff records and settings is unnecessary; the owner decides. |
| Me (the admin) | User support and password resets | /Administration | IT-Support | Help Desk Admin | Needs limited user support tools; full control could change security and business settings; the owner decides. |

## The partner's cold read

Partner: pending real partner review.
One person with more than the job needs, or "none" and why: pending review.
