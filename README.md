# CICBv2 Release Notes

---

## 2026-01-12 - v2.3.2.65

[Added]
- **Winget Automation**: Added manifests and submission support for v2.3.2.65.

[Changed]
- **Docs**: Added standard Copilot instructions for development consistency.

---

## 2026-01-12 - v2.3.2.64

[Changed]
- **Deploy Manager**: Refined log output colors for improved readability.

---

## 2026-01-12 - v2.3.2.63

[Internal]
- **Build**: Internal build / Version increment skipped in git history.

---

## 2026-01-12 - v2.3.2.62

[Internal]
- **Build**: Internal build / Version increment skipped in git history.

---

## 2026-01-12 - v2.3.2.61

[Internal]
- **Build**: Internal build / Version increment skipped in git history.

---

## 2026-01-12 - v2.3.2.60

[Added]
- **Server**: Added support for synchronization of 'Alarm Type' and 'Setting Name' fields from the portal.

---

## 2026-01-12 - v2.3.2.59

[Added]
- **Server**: Enhanced Portal Alarm synchronization to support parsing and persisting all alarm fields (Message, Color, Sound, Loop, Blink).
- **Server**: Implemented database schema updates to store synchronized alarms locally.
- **Server**: Added logic to seamlessly replace existing alarm settings and handle unnamed alarms sequentially during sync.

---

## 2026-01-12 - v2.3.2.58

[Added]
- **Server**: Initial implementation of Portal Alarm synchronization to local database.

[Fixed]
- **Build**: Resolved `NOMINMAX` macro redefinition warnings in Windows builds.

---

## 2026-01-11 - v2.3.2.57

[Changed]
- **Server**: Restricted activation of Portal Alarms to occur only when the Server is manually toggled into **Alarm Mode**.

---

## 2026-01-11 - v2.3.2.56

[Added]
- **Server**: Implemented support for parsing individual client alarms from the web portal API.
- **Server**: Added logic to propagate portal-defined alarms (message, color, sound, loop) to specific clients. **Note**: Portal alarms only activate when the Server is manually toggled into **Alarm Mode**.
- **Deploy Manager**: Enhanced log output with color-coded status messages (Green for success, Red for failure) for better visibility.

[Fixed]
- **Client & Server**: Resolved deprecated Qt API warnings (`QWebSocket::error` -> `errorOccurred`, `qChecksum` overloads) to improve codebase stability and compatibility with newer Qt 6.x versions.

---

## 2026-01-11 - v2.3.2.53

[Fixed]
- **Winget Automation**: Critical fix for submission script to base new branches off `upstream/master` instead of `origin/master`. This ensures clean commit history for Pull Requests to the official Microsoft Winget repository.

---

## 2026-01-11 - v2.3.2.52

[Added]
- **Winget Automation**: Official release submitted to `winget-pkgs`.
- **Winget Automation**: Introduced `submit-to-winget.ps1` to fully automate the submission process, including:
  - Automatic detection of latest build.
  - SHA256 hash calculation.
  - Manifest generation/update (Version, URL, Hash).
  - Git automation for branching and pushing to fork.

[Changed]
- **Deployment**: Consolidated all Winget helper scripts (`exe-helper`, `guid-helper`, `prepare-winget`) into the single master submission tool.

---

## 2026-01-11 - v2.3.2.51

[Fixed]
- **Deploy Manager**: Fixed parameter passing for timeout arguments in the backend PowerShell script.
- **Winget Manifests**: Corrected schema validation issues in manifest templates.

[Changed]
- **Config**: Removed unused legacy encryption keys (`LEGACY_AES_KEY`, `LEGACY_AES_IV`) from environment configuration to improve security posture.

---

## 2026-01-11 - v2.3.2.50

[Internal]
- **DevOps**: Refactoring of deployment scripts to support modular Winget submission.
- **DevOps**: Cleaned up obsolete build artifacts and temporary helper scripts.

---

## 2026-01-11 - v2.3.2.49

[Added]
- **Deploy Manager**: Added configurable timeouts for signing operations.
  - **Installer Sign Timeout**: Default 120 seconds.
  - **MSI Sign Timeout**: Default 30 seconds.
- **UI**: Added Settings dialog to configure these timeouts persistently.

[Improved]
- **Signing**: Enhanced reliability of signing process on slower network connections or when timestamp servers are experiencing latency.

---

## 2026-01-11 - v2.3.2.48

[Added]
- **MSI Installer**: Desktop shortcuts for Client, Server, and CCM now created on installation.
- **Deploy Manager**: Abort functionality - Deploy button changes to red "Abort" button during deployment process.

[Changed]
- **MSI Installer**: Installation structure now matches EXE installer - all files install directly to `C:\Program Files (x86)\CICBv2\` without subfolders.
- **MSI Build Process**: Uses separate flat staging directory to ensure clean file structure without inno-setup folder.
- **Deploy Manager**: Deploy button now changes text and color (red #F44336) during active deployment, allowing user to abort.

[Fixed]
- **MSI Installer**: Icon path corrected to reference flat directory structure.

---

## 2026-01-11 - v2.3.2.47

[Added]
- **Deploy Manager**: Auto-increment version system - version now automatically increments on each build.
- **Deploy Manager**: Single instance enforcement using QSharedMemory to prevent multiple instances.
- **Deploy Manager**: Log timestamps - each log entry now shows [HH:mm:ss] timestamp with improved line spacing.
- **MSI Installer**: Fixed packaging to include all dependency files (Qt DLLs, plugins, configs) using WiX heat.exe harvesting.
- **MSI Installer**: Optional auto-startup features for both Client and Server (enabled by default, can be deselected).
- **Inno Setup Installer**: Optional auto-startup tasks for Client and Server with checkedonce flag.
- **Documentation**: Comprehensive MSI Installation Guide (`MSI_INSTALLATION_GUIDE.md`) for IT administrators covering silent installation, Group Policy deployment, and troubleshooting.

[Changed]
- **Deploy Manager UI**: Simplified interface by removing 5 checkboxes (Full, WinGet, WingetSign, MsiSign, InstallerSign).
- **Deploy Manager UI**: Auto-combine "Create Installer" with signing and "MSI" with signing.
- **Deploy Manager UI**: Reorganized layout - Production/Protection/Sign Binaries in one row, Create Installer/MSI in second row.
- **Deploy Manager UI**: All buttons styled with green color scheme (#4CAF50) with hover/pressed effects.
- **Deploy Manager**: MSI checkbox now checked by default.
- **WinGet**: Transitioned from EXE to MSI-only approach for WinGet publication.

[Fixed]
- **WiX Installer**: Resolved CNDL0062 error (Component Directory conflict) by restructuring ComponentGroups.
- **WiX Installer**: Resolved LGHT0091 error (duplicate ComponentGroup definition) by removing manual ProductComponents.
- **MSI Packaging**: Fixed missing dependencies issue - MSI now includes all required files via automated harvesting.

[Technical]
- **Build System**: Implemented `increment_version.cmake` for automatic version management.
- **Auto-Startup**: Registry keys added to HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run for optional auto-launch.
- **WiX Integration**: Automated file harvesting using heat.exe with -cg ProductComponents -dr INSTALLFOLDER -gg -sfrag -srd -sreg flags.

---

2026-01-05 - v2.3.2.6

[Fixed]
- CCM (Client Configuration Manager) startup performance optimized.
- Server UI: Group Name input field was disabled in the "Add Group" section.

[Improved]
- Deployment Manager: Added retry logic for file signing to prevent file lock errors.
- Documentation: Corrected default port (56789) in Server as Service guide.

---

2026-01-05 - v2.3.2.5

[Added]

• Native Windows Service support for Server.
  - The server can now be run as a native service using the `-service` flag.
  - Removed dependency on third-party service wrappers (NSSM).

---

2026-01-05 - v2.3.2.2

[Changed]

• Refactored data storage to use Machine-Wide Shared Data model.
  - Data is now stored in `C:\ProgramData\ClassificationBanner\` instead of the installation directory.
  - Ensures better compatibility with multi-user environments and security best practices.

[Improved]

• Deploy Manager UI updates.
• Installer signing logic optimization (batch signing).

---

2025-12-28 - v2.3.1.87

[Fixed]

• Linux: Window flags and banner struts issues.
• Linux: Console visibility bug.

---

2025-12-20 - v2.3.1.80

[Fixed]

• Linux: Tray Icon interaction issues.
• Bug where right text was forced to be common across all screens.

[Improved]

• Documentation and diagrams for Qt project structure.

---

2025-12-10 - v2.3.1.0

[Added]

• Linux Support: Cross-platform CMake config, Linux Banner, and GNOME extension integration.

[Changed]

• Renamed build scripts for cross-platform consistency (`deploy.ps1`).

---

2025-08-07 - v2.2.2.1 (internally released)

[Fixed]
- CICB-Server certificate parsing issue.

---

2025-07-17 - v2.2.2.0 (internally released)

[Improved]
- CICB-Server now can support package features.

---

2025-04-22 - v2.2.1.2 (internally released)

[Fixed]
- CICB-Banner cannot adapt to the Windows tablet mode bug.
- CICB-Client/CCM group name save bug.
- CICB-Server/Client version mismatch bug.
- CICB-Banner cannot adapt to changes in Windows screen resolution due to a bug.
- CICB-Banner cannot adapt to the Windows scaling changes bug.

---

2025-01-24

[Released]
- CICB-ServiceInstaller - v1.01.

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

2023-03-17 - v2.1.1.9

[Released]
- Internal release.

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

2022-08-31 - v2.0.8.0

[Released]
- Internal release.

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

2022-08-12 - v2.0.5.0

[Released]
- Internal release.

---

2022-08-03 - v2.0.4.0

[Fixed]
1. LDAP toggle button issue.
2. LDAP is not able to sync with the LDAP server.

---

2022-07-28 - v2.0.3.0

[Released]
- Internal release.

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
