# CICBv2 Release Notes

2025-04-13 - v2.2.1.2 (internally released)

[Fixed]
- CICB-Client CCM group name save issue.
- CICB-Server/Client version mismatch issue.

---

2025-01-24 - v1.01

[Released]
- CICB-ServiceInstaller.

---

2024-11-08 - v2.2.1.1 (internally released)

[Fixed]
- CICB-Client CCM CLI argument issue.

---

2024-06-10 - v2.2.1.0 (internally released)

[Fixed]
- CICB-Server license activation bug.

---

2024-06-06 - v2.2.0.1 (internally released)

[Fixed]
- CICB-Server certificates bug.

---

2024-06-30 - v2.2.0.0

[Updated]
- CICB Windows.
- CICB Portal.
- Public key.

[Added]
- Single license activation support.
- Added certificates system.

[Fixed]
- Message term inconsistency.
  
[Download]
- OS: Windows 10+
- OS: Linux Ubuntu 16.8+ / Debian 8+
- Algorithm: SHA256

### !!! IMPORTANT !!!
Starting from version CICB-v2.2.0.0, a new Control Panel (cp.cyberintelsystems.com) is used for license management and issuance. The old CICB-v2.1.2.3 and earlier versions still use the old Portal (portal.cyberintelsystems.com). Please note that the changes between the two versions are significant, making them incompatible. Please consider upgrading carefully.

---

2023-11-17 - v2.1.2.3

[Fixed]
- Server minor license issue.
  
[Download]
- OS: Windows 7+ or Windows Server 2018+
- Algorithm: SHA256
- Hash: 91A20EA092A16F7711EF8B252A00BD02538E5EA15A4D4D39CF8236C2760E9119

---

2023-09-25 - v2.1.2.2

[Improved]
- Server license verification frequency.
  
[Released]
- Executable installer.
  
[Known Issue(s)]
- The installer menu shortcut creation was incorrect. We will fix it in the next release.

[Download]
- OS: Windows 7+ or Windows Server 2018+
- Algorithm: SHA256
- Hash: E74E0F3192B7DF854C73C55AE6684E4548370EEBDEB1348476FD990F2FC203AA

---

2023-09-05 - v2.1.2.1

[Fixed]
- Banner displays incorrectly in Windows 11 when the scale is not 100% dpi.

---

2023-04-17 - v2.1.2.0

[Fixed]
- Windows Server 2022, no license issue.

---

2023-02-25 - v2.1.1.8

[Added]
1. CICBv2 Installer
2. Server About System Tray Menu
  
[Fixed]
1. CCM cannot save the client.connection and group.settings files within the same folder.
2. CCM displays the wrong default group information.

---

2023-02-25 - v2.1.1.8

[Added]
1. CICBv2 Installer
2. Server About System Tray Menu
   
[Fixed]
1. CCM cannot save the client.connection and group.settings files within the same folder.
2. CCM displays the wrong default group information.

---

2023-02-15 - v2.1.1.7

[Fixed]
1. CA signed the client with a valid publisher's certificate.
2. CA signed the server with a valid publisher's certificate.

---

2023-01-30 - v2.1.1.6

[Fixed]
- client.connection lost after each computer reboot.

---

2022-12-27 - v2.1.1.5

[Fixed]
1. CCM cannot save the previous value.
2. CCM cannot decrypt the server API key correctly.

---

2022-12-08 - v2.1.1.4

[Fixed]
1. Server updates compare version issues.
2. Multi-%scale issue.
   
[Added]
- Client update with batch deployment.

---

2022-11-25 - v2.1.1.3

[Added]
1. Enabled the Update button for the server.
2. Added PowerShell batch updater.ps1 sample file.
   
[Updated]
1. Renamed Client Service -> Client
2. Renamed Client Banner -> Banner
3. Renamed Service Agent -> Server

---

2022-10-18 - v2.1.1.2

[Fixed]
1. Win11 banner display scaling setting issue.
2. System tray icons bug.
3. CCM display scaling setting issue.

---

2022-10-11 - v2.1.1.1

[Fixed]
1. Missing left text for demo mode.
2. The new group is missing default screen settings.
3. The default color for the banner and text is missing.
4. The banner displays a 0/1 placeholder issue when the display option turns off.

---

2022-10-05 - v2.1.1.0

[Fixed]
1. Random screen with the banner.
2. Lost screen settings.

---

2022-09-27 - v2.1.0.0

[Added]
- Sectigo Digital signed.
  
[Fixed]
1. The version displays incorrectly after startup.
2. License and settings do not display correctly after startup.

---
2022-09-23 - v2.0.9.0

[Fixed]
1. Agent startup.
2. Client startup.
   
---

2022-08-25 - v2.0.7.0

[Fixed]
- Banner display incorrectly when the system scale is not 100%.

---

2022-08-15 - v2.0.6.0

[Fixed]
1. Startup issue.
2. Missing DLL file issue.

---

2022-08-03 - v2.0.4.0

[Fixed]
- LDAP toggle button issue.
- LDAP is not able to sync with the LDAP server.

---

2022-08-03 - v2.0.4.0

[Fixed]
1. LDAP toggle button issue.
2. LDAP is not able to sync with the LDAP server.

---

2022-07-20 - v2.0.2.0

[Fixed]
1. CCM API key issue.
2. Client and Agent communication issue.

---

2022-07-20 - v2.0.2.0

[Fixed]
1. CCM API key issue.
2. Client and Agent communication issue.

---

2022-07-15 - v2.0.1.0
[Fixed]
- Client IPv4 display issue.

---

2022-07-10 - v2.0.0.0

[Release]
- Release for NPO users.
