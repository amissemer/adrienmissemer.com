---
layout: page
title: Personal Finance App — Privacy Policy
permalink: /personalfinanceapp/privacy/
published: true
---
This page describes how personal data is handled by a private personal finance application. See also the [Terms of Use](/personalfinanceapp/terms/).

Effective date: 2026-09-04. Last updated: 2026-09-04.

### What the application is

It is a command-line tool that I run on my own Mac to keep track of my family's net worth and cash flow. It is not published, it has no sign-up, no server, no website and no cloud backend. There are no users other than me and consenting members of my family. It is not offered to the public and it is not a commercial service.

It reads account information through [Enable Banking Oy](https://enablebanking.com/), a Finnish licensed account information service provider (AISP) under PSD2, which connects to the account holder's own bank — BoursoBank in France. Access is read-only account information: balances and transaction history. The application never initiates payments.

The data flow is: bank → Enable Banking → my personal Mac. It stops there. Nothing is uploaded anywhere, and no analytics are run on the data.

### Who is responsible

The data controller is Adrien Missemer, acting in a personal capacity, in Montreal, Quebec, Canada.

There is no data protection officer — this is a household tool, not an organisation. For any question about this policy or about your data, write to `adrien.missemer+privacy@gmail.com`.

### What personal data is processed

* Account holder name
* Account identifiers, including IBAN
* Account balances
* Transaction records: date, amount, counterparty name, and remittance information or description

The data subjects are me and consenting family members. No third party's data is collected deliberately, although transaction records naturally contain the names of counterparties I or my family have transacted with.

### Why it is processed

The sole purpose is personal and family net-worth and cash-flow tracking.

There is no profiling, no advertising, no automated decision-making, no sale of data and no onward sharing with anyone.

### Legal basis

Consent, under Article 6(1)(a) GDPR. Consent is given per bank connection through the bank's own strong customer authentication (SCA) flow, and it can be withdrawn at any time.

Because this processing is carried out by a natural person for purely personal and household purposes, the household exemption in Article 2(2)(c) GDPR may well apply. This policy is provided regardless, so that anyone whose data is involved can see exactly what happens to it.

### Who receives the data

* Enable Banking Oy (Finland), acting as the regulated account information service provider
* The account holder's own bank, which is the source of the data

No one else. There is no hosting provider, no analytics vendor and no sub-processor beyond these.

### Transfer outside the EEA

**The data originates from French bank accounts and is stored on a personal computer located in Canada.** This is a transfer of personal data outside the European Economic Area, and it is the most significant thing to understand about this setup.

Canada's adequacy decision covers organisations subject to PIPEDA in the course of commercial activity. This is a private, non-commercial household activity, so I do not claim that the adequacy decision applies to it. The transfer happens because the account holders are also the people running the tool and consenting to it: it is a person accessing their own bank data on their own computer, which happens to be in Canada.

### Storage and security

The data is stored locally on a personal computer with full-disk encryption (FileVault) enabled. Credentials and access tokens are held encrypted at rest. There is no server and no cloud backup of the financial data.

### How long it is kept

Data is kept until I delete it. There is no automatic retention schedule, because there is no organisation to enforce one.

Consent can be withdrawn at any time — both in the bank's own interface, where third-party access can be revoked, and by deleting the session through Enable Banking. Withdrawing consent stops any further data being retrieved.

### Your rights

Anyone whose data is processed here has the right to request access, rectification, erasure, restriction of processing, portability, and to object to the processing, as well as to withdraw consent at any time. Since the entire dataset lives in files on one computer, these requests are handled directly and quickly. Use the contact address given above.

You also have the right to lodge a complaint with a supervisory authority. Because the accounts are French, the competent authority is the CNIL: [https://www.cnil.fr](https://www.cnil.fr).

### Cookies and tracking

The application itself sets no cookies and runs no analytics.

This website no longer uses Google Analytics — it was removed entirely on 2026-09-04. One third-party request does remain: the avatar in the site header is loaded from Gravatar (`www.gravatar.com`, operated by Automattic), which means Gravatar receives your IP address on every page view of this site.

### Changes to this policy

If the setup changes — a different bank, a different provider, a different location for the machine — this page will be updated and the "last updated" date above will change.
