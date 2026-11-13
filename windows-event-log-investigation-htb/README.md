# Windows Event Log Investigation — HTB Logjammer

Hello, I'm Joel, in this case I'll take the role as a DFIR (Digital Forensics and Incident Response), this lab focused on analysing Windows Event Logs, documenting, so I'm gonna supporting evidence, and explaining the security implications of observed activity.

The investigation is tracked in Jira and documented through
reproducible searches, relevant screenshots, and evidence references.

## Scenario

Forela-Security has provided a technical assessment for a DFIR consultant role. The assessment requires examining supplied Windows Event Logs and answering questions about the activity recorded in those artifacts.

This htb project documents my investigation process, including how I locate relevant events, interpret their fields, and distinguish confirmed observations based in my hypothesis.

## Investigation Objectives

- Identify the evidence relevant to the htb questions.
- Examine recorded user activity and system configuration changes.
- Analyse relevant Security, System, PowerShell, Windows Defender,
  and Windows Firewall events.
- Correlate related events where shared identifiers and context
  support the relationship.
- Build a timeline of relevant observations.

## Ticket Jira

The ticket is reviewed in Jira, ownership is taken, and the investigation begins. The directory containing the log files is downloaded and ingested into Splunk for analysis.

![Jira Ticket](screenshots/01_ticket_jira.png)

![Logs insert in Splunk](screenshots/00_logs_inSPlunk.png)

## Validate logs in Splunk

I ingest these `.evtx` log files into Splunk in JSON format. At this point I change the time to UTC time.
As I know, the suspicious user is `cyberjunkie` and I'm dealing with Windows event logs.
So I'll start looking for event ID `4624`, which means a successful logon attempt.

Important note: Windows event IDs are not unique, and since I'm working with multiple log sources, I'll be interested in Security logs for this purpose.

![Security Logs](screenshots/02_security_logs.png)

In my case, the event code I'm interested in has the name `Event.System.EventID`. So I got 67 events with code 4624, but if I filter by `cyberjunkie` I receive 4 events, and most importantly, I got this first successful logon attempt from `cyberjunkie` at `27/03/2023 14:37:09`.

![First success login](screenshots/03_login_4624.png)

## Bypass defenses and persistence

At this point I need to understand how it bypassed the defense system, so manually I'll look for event codes in the Windows Firewall logs. For example, event code `2004` means a rule was added to the firewall. I got `490` such events, but I can't say that the user `cyberjunkie` did it. However, filtering by `userId` I got `29` added events from this user, so I can confirm that `cyberjunkie` is responsible for making these changes to the firewall rules.

![Firewall added by cyberjunkie](screenshots/04_firewall_added.png)

So looking in the logs, the rule name that had been added was `Metasploit C2 Bypass` on `2023-03-27 14:44:43`, and the direction is `2`, which means `Outbound`.

So with this information I'll update the Jira ticket with the new information, to share it with my "team".

![Jira update news](screenshots/05_jira_update.png)

