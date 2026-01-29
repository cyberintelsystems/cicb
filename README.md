# CICBv2 Release Notes

---

## 2026-01-28 - v2.7.7

[Fixed]
- **CCM**: Fixed critical issue where banner wouldn't update after CCM saves new group name until manual Client restart.
  - CCM now correctly finds Client window using actual window title 'Cyber Intel Classification Banner - Client'
  - Implemented PID-based window enumeration with fallback matching for both title patterns
  - Added comprehensive debug logging for window discovery process
  - Banner now updates immediately when settings are saved in CCM without requiring manual restart

[Technical Details]
- Enhanced IPC communication reliability between CCM and Client using `WM_USER+401` message
- Improved window enumeration logic to handle hidden Qt windows
- Added `EnumWindowsProcCCM` callback with `GetWindowThreadProcessId` for precise window identification
- Fixed window title mismatch issue (programmatic vs UI-defined titles)

---

## 2026-01-27 - v2.6.75

[Fixed]
- **CCM**: Fixed license parsing issue (PID 4) to correctly support distributed licensing.

---

## 2026-01-27 - v2.6.71

[Fixed]
- **Release**: Enhancements to the release automation script.
- **Server**: Optimized network interface enumeration to resolve high CPU usage and potential freezing.
- **Client**: Added fallback to `*default` group if configuration is missing or invalid.
- **Release**: Improved artifact cleanup to exclude debug and environment files.
- **Docs**: Ensure installation guides are correctly placed in the `docs` folder.

---

## 2026-01-26 - v2.6.69

[Fixed]
- **Server**: Optimized network interface enumeration to resolve high CPU usage and potential freezing.
- **Client**: Added fallback to `*default` group if configuration is missing or invalid.
- **Release**: Improved artifact cleanup to exclude debug and environment files.
- **Docs**: Ensure installation guides are correctly placed in the `docs` folder.

---

## 2026-01-26 - v2.6.41

[Fixed]
- **CCM**: Fixed OpenSSL `applink` error causing crashes on launch by adding a wrapper.
- **CCM**: Fixed Windows Game Bar popup appearing over CCM by adding a manifest with declared `DesktopApp` type and disabling Game Bar.
- **Release**: Improved build script to prevent version bumps on failure.
- **License**: Refactored PID verification to support remote clients and enable checks based on `client.connection` (Distributed Architecture Support).

---

## 2026-01-26 - v2.6.19

[Added]
- **Flutter CICBv2**: Added complete Flutter-based implementation of Classification Banner system as an alternative to Qt.
  - Banner: Flutter-based banner display application
  - CCM: Client Control Manager for group selection
  - Client: Client application for banner management  
  - Server: Server application for centralized control
  - UI Editor: Configuration UI for banner customization
  - Build and deployment scripts (build_all.ps1, deploy_all.ps1)
  - Version management and release build infrastructure
- **Banner**: Added group database ID display in Banner window title for easier troubleshooting.
- **Debug Tools**: Added Python diagnostic utilities for color verification and database inspection.

[Fixed]
- **Banner**: Fixed critical color rendering bug where RGB integers were incorrectly parsed as hexadecimal strings.
  - Issue: Integer value 13216 (0x33A0) was being parsed as hex string "13216" resulting in 0x13216 = 78358
  - Fix: Modified `parseColorToInt()` to check QVariant type first, only parse strings as hex with "0x" or "#" prefix
- **Banner**: Fixed missing RGB to BGR color conversion for text rendering (line 746 in wnd_proc.cpp).
  - Windows COLORREF expects BGR byte order (0x00BBGGRR) but database stores RGB (0x00RRGGBB)
  - Added proper conversion: `RGB((color >> 16) & 0xFF, (color >> 8) & 0xFF, color & 0xFF)`
- **Banner**: Colors now display correctly - dark blue (#0033A0) banner with white (#FFFFFF) text for *confidential.
- **CCM**: Enforced PID 3+ license requirement for changing classification groups.

[Security]
- **Encryption**: Completed migration from SimpleCrypt to AES-256-GCM encryption for client-server communication.
- **Encryption**: Database encryption temporarily disabled in development for debugging (startTransaction/endTransaction).

[Documentation]
- **Docs**: Moved documentation files to Qt/docs folder for better organization.
- **Docs**: Added comprehensive debug logging documentation (DEBUG_LOGGING.md).
- **Docs**: Added banner performance and language documentation.
- **Docs**: Added feasibility analysis and project roadmap.

[Technical Details]
- Qt Version: 6.10.1 with MinGW
- Flutter Implementation: Complete parallel implementation with cross-platform support
- Database: SQLite with AES-256-GCM encryption (temporarily disabled for development)
- Color Fix: Fixed `parseColorToInt()` in Qt/server/datamanager.cpp (lines 13-35)
- Color Fix: Fixed text rendering in Qt/banner/wnd_proc.cpp (line 746)
- Version Management: Scripts for automated version increments and build management

---

## 2026-01-19 - v2.4.48

[Fixed]
- **Release Script**: Detailed release report now uses Yellow for "Unknown" status instead of Red, improving readability of non-critical checks.
- **Server**: Fixed runtime side-by-side configuration error handling; enforced stricter validation and normalization for predefined group names (must be lowercase and start with '*').
- **Release Manager**: Improved log readability by changing the separator line color to white.

[Technical Details]
- Server: Added `normalizePredefinedGroupName` to standard `*groupname` format.
- Release Manager: Updated `appendLog` to support custom styling for separators.

---

## 2026-01-18 - v2.4.42

[Added]
- **Release Manager**: Added "GitHub Release Retention" setting to automatically manage and clean up older releases on GitHub.

[Fixed]
- **Release Automation**: Fixed syntax errors in release script and improved GitHub release publishing flow.

---

## 2026-01-18 - v2.4.35

[Fixed]
- **CCM**: Enforced single instance execution. The application now checks for existing instances on startup and prevents multiple copies from running simultaneously.
- **CCM**: Fixed configuration path inconsistency. CCM now correctly saves `group.settings` and `client.connection` to the shared `ProgramData` directory (instead of `Documents`), ensuring the Client application can locate and read the configuration.
- **Banner**: Prevented "Xbox Game Bar" popup on Windows by adding an application manifest and explicitly identifying `banner.exe` as a desktop application.
- **Release**: Enhanced release script robustness with improved directory cleaning, file locking handling, and better error reporting for the code signing process.

[Technical Details]
- CCM: Implemented `QSharedMemory` check on startup with key "CCM_Single_Instance_Key_12345".
- CCM: Switched `mCurrDir` from `QStandardPaths::DocumentsLocation` to Application Directory logic, and updated file save paths to use `CICBUtil::getSharedDataPath()`.
- Release Script: Added retry loops (up to 5 attempts) for directory cleaning and file copying steps to mitigate "Access Denied" errors caused by OS file locking.

---

## 2026-01-18 - v2.4.30

[Fixed]
- **Banner**: Fixed decryption issue where CUI settings (Group Name) were displaying garbage characters.
- **Release**: Improved release report output formatting for better readability.

[Technical Details]
- **OpenSSL**: Changed server-side encryption padding from default (PKCS7) to `EVP_CIPHER_CTX_set_padding(ctx, 0)` (Zero Padding) to match client-side decryption logic.

---

## 2026-01-18 - v2.4.12

[Added]
- **Release Manager**: Updated Release Manager to v2.4.12.
- **Licensing**: Added support for PID 0 ("Free" Plan) predefined groups.
- **Release**: Added configurable signing delay setting.

---

## 2026-01-17 - v2.3.93

[Added]
- **Configuration**: Added support for externalized `default_settings.json` to allow customizing "protected default groups" without recompiling.

[Fixed]
- **Build**: Resolved build errors related to `m_productID`.

---

## 2026-01-17 - v2.3.91

[Security]
- **Licensing**: Enhanced "Protected Default Group" logic to respect license expiration.

---

## 2026-01-17 - v2.3.90

[Added]
- **Feature Registry**: Implemented centralized Feature Registry system to manage feature lockdown based on Plan IDs.
- **Alarms**: Enabled alarms for PID 3 (Enterprise).

[Security]
- **Configuration**: `settings.json` is now embedded as a Qt resource to prevent tampering.

---

## 2026-01-16 - v2.3.59

[Improved]
- **Release Manager**: UI improvements.
- **Documentation**: Fixed service documentation paths.

---

## 2026-01-15 - v2.3.56

[Fixed]
- **Banner Performance**: Fixed critical CPU performance issues causing excessive CPU usage:
  - Added `Sleep(1)` to animation busy-wait loop, reducing CPU from 100% to <5% during window sliding animations
  - Moved `SetWindowPos()` inside alarm check to eliminate 8+ unnecessary window system calls per second on multi-display setups
  - Optimized `InvalidateRect()` calls to only execute during alarm state, preventing continuous unnecessary repaints

[Changed]
- **Themida Protection**: Enabled VM support (`OPTION_PROTECTION_IS_VMWARE_SUPPORT=true`) for all executables (Server, Client, Banner, CCM, CCM-Lite) to allow CICB to run on virtual machines, VDI, RDP, Azure Virtual Desktop while maintaining hardware-based identification for licensing.

[Technical Details]
- Banner animation loop was using tight busy-wait without yielding CPU: `while (GetTickCount() < timeout) { SetWindowPos(); UpdateWindow(); }`
- Added 1ms sleep between animation frames to prevent CPU saturation while maintaining smooth 60+ FPS animation
- `TimerProc()` was calling `SetWindowPos(HWND_TOPMOST)` every second for all windows regardless of alarm state
- VM detection was blocking execution on VMware, Hyper-V, VirtualBox, Citrix - now hardware ID collection still works in VM environments

---

## 2026-01-15 - v2.3.55

[Added]
- **Documentation**: Created comprehensive feature lockdown documentation (`Qt/docs/feature-lockdown-by-plan.md`) detailing PID-based licensing structure with 5 tiers (Free, Basic, Professional, Enterprise, Government) and complete feature matrix showing capabilities for each plan.

[Changed]
- **License Plans**: Restructured Free plan (PID 0) from 30-day trial to 1-year renewable license with feature limitations:
  - Limited to 2 displays per workstation
  - Disabled banner customization (colors, font, border size, text content)
  - Disabled LDAP/AD integration and 3rd-party API access
  - Disabled logging, alarms, and manual controls
  - Community support only
- **Feature Matrix**: Consolidated and organized 48 features across 7 categories (Licensing, Banner Display, Management, Integration, Security, Logging, Deployment, Support)
- **Display Limits**: Defined display support per plan (Free=2, Basic=4, Professional=6, Enterprise/Government=12)
- **Client Support**: All plans now use certificate-based client limits (max 30,000) instead of fixed tiers

[Improved]
- **Documentation**: Added detailed feature descriptions including technical specifications, compliance standards (FIPS 201, FISMA, DISA STIGs), and real-world use cases
- **Documentation**: Synchronized feature matrix with live pricing page (cyberintelsystems.com/pricing)

---

## 2026-01-15 - v2.3.54

[Fixed]
- **System Info**: Fixed missing CPU and RAM information in logs by replacing deprecated `wmic` commands with PowerShell `Get-CimInstance` commands for Windows 11 compatibility.

[Technical Details]
- `wmic` commands were timing out on Windows 11 (deprecated in favor of PowerShell)
- Replaced with `Get-CimInstance -ClassName Win32_Processor` for CPU name
- Replaced with `Get-CimInstance -ClassName Win32_ComputerSystem` for total physical memory
- Added 5-second timeout and proper error handling
- System info now displays correctly: `OS=Windows 11 Version 25H2, CPU=Intel(R) Xeon(R) w7-2475X, RAM=511.47 GB`

---

## 2026-01-15 - v2.3.47

[Fixed]
- **Server**: Fixed binary data in group names causing banner crash by sanitizing decrypted group names before sending to clients, removing null bytes and control characters that corrupted command-line arguments.

[Technical Details]
- Server was sending binary data embedded in group names (e.g., `*Default\x00\x00...`) to clients
- Clients would append this corrupted group name to banner arguments, causing "Insufficient arguments" error
- Solution: Added `QRegularExpression` sanitization on server-side after group name decryption to remove control characters (`\x00-\x1F`)

---

## 2026-01-15 - v2.3.45

[Fixed]
- **Client**: Fixed banner process crash on second launch caused by binary data and null bytes in user profile/group names being passed as command-line arguments. Banner now properly validates and receives all 12 expected arguments.
- **Client**: Resolved "Insufficient arguments. Exiting." error by sanitizing group name data before passing to Banner process, removing control characters (`\x00-\x1F`) that corrupted argument parsing.

[Improved]
- **Client**: Enhanced argument sanitization at multiple levels - during group name construction and in `runAppbar()` function - ensuring robust command-line parsing for Banner subprocess.
- **Qt 6 Compatibility**: Migrated from deprecated `QRegExp` to `QRegularExpression` for binary data removal, ensuring compatibility with Qt 6 framework.

[Technical Details]
- Banner splits arguments using `"--"` delimiter and expects exactly 12 arguments (screen index, dimensions, colors, text strings, monitor name)
- When user profile data containing null bytes was appended to `linfo` parameter, command-line parsing failed, reducing argument count from 12 to 4
- Solution: Added `QRegularExpression` sanitization to remove null bytes and control characters from group names before banner launch

---

## 2026-01-14 - v2.3.43

[Fixed]
- **Banner**: Fixed duplicate text rendering issue where right-aligned text was rendered twice causing overlapping display (e.g., "SERVER DOWNS" appearing duplicated).
- **Server**: Enhanced license validation with ±1 day tolerance for timezone differences, preventing "Not Yet Valid" errors when certificates activate on dates with timezone offsets.

[Improved]
- **Deploy Manager**: Now reads version dynamically from `version.ver` file instead of compiled constant, ensuring version display matches current build.
- **Deploy Manager**: Changed output directory from `build/win/archives` to `build/deploy-manager` for better organization.
- **Deployment**: SmartCardManager.exe is now excluded from release archives and deployment packages.
- **Themida Protection**: Optimized server protection for 60-75% faster startup (8-12s → 2-4s estimated) by disabling heavy features while keeping essential security (anti-debug, anti-patching, integrity checks).

[Added]
- **MSI Installer**: Created comprehensive installation guide (`MSI-INSTALL-GUIDE.md`) documenting silent installation with auto-startup features for Client and Server.
- **Documentation**: Added `OPTIMIZATION-NOTES.md` documenting Themida configuration changes and security trade-offs.
- **Winget Automation**: Enhanced submission script to automatically generate clickable GitHub PR URLs with optional `-OpenPR` parameter to open browser automatically.

[Changed]
- **UI**: Deploy Manager button changed from green → purple → dark purple (#6A1B9A) for improved visual design.
- **UI**: Fixed Deploy Manager button height inconsistency by removing padding from stylesheet.

---

## 2026-01-14 - v2.3.25

[Fixed]
- **Server**: Fixed decryption failures (error:1C800064:Provider routines::bad decrypt) caused by EVP_CipherFinal_ex attempting to verify padding that clients don't add. Server now matches client encryption pattern by processing data with EVP_CipherUpdate only, maintaining backward compatibility with legacy client code that never calls EVP_CipherFinal_ex.

[Technical Details]
- Client/CCM encryption uses legacy OpenSSL pattern: EVP_CipherUpdate() without EVP_CipherFinal_ex()
- Server decryption incorrectly added EVP_CipherFinal_ex() which expects properly padded blocks
- 128-byte messages (8 AES-128-CBC blocks) would decrypt 112 bytes (7 blocks) successfully but fail on the 8th block during padding verification
- Solution: Removed EVP_CipherFinal_ex() from server decryption to match client behavior

---

## 2026-01-14 - v2.3.23

[Fixed]
- **Server**: Fixed certificate date validation that incorrectly subtracted 1 day from `notBefore`, causing "License Not Yet Valid" errors for certificates starting on future dates.
- **Deploy Manager**: Updated status bar to show version number in deployment states ("Deploying v2.3.23..." and "Done v2.3.23").

---

## 2026-01-14 - v2.3.22

[Fixed]
- **Server**: Fixed certificate date parsing to support both UTCTime (2-digit year) and GeneralizedTime (4-digit year) formats using `ASN1_TIME_to_tm()` for proper year 2026+ certificate validation.
- **Server**: Fixed decryption buffer overflow by using dynamic buffer allocation based on input size instead of hardcoded 1024-byte limit.
- **Server**: Fixed CSS parser warnings for invalid `rgba()` syntax by adding missing alpha channel values in Qt stylesheets.
- **Server**: Enhanced OpenSSL error reporting with `ERR_get_error()` and `ERR_error_string_n()` for better decryption failure diagnostics.

[Improved]
- **Server**: Certificate selection now uses actual expiration date (`notAfter`) instead of filename timestamp, automatically selecting the certificate valid longest when multiple certificates exist for same server ID.
- **Server**: Added detailed logging during certificate selection showing expiration dates and selected certificate path.

[Changed]
- **Versioning**: Migrated from 4-part version format (2.3.3.7) to 3-part semantic versioning (2.3.22), simplifying version increments to patch-only updates.

---

## 2026-01-14 - v2.3.2

[Fixed]
- **Server**: Fixed license validation failing for certificates with uppercase `PUBKEY:` and `CRL:` prefixes by implementing truly case-insensitive matching.
- **Debug**: Relocated debug control files (`debug.on`, `debug.key`) from application directory to user Documents folder for consistent location with `debug.log`.

[Improved]
- **Server**: Enhanced certificate validation error logging with detailed diagnostics, hex dumps, and possible root causes for easier troubleshooting.
- **Server**: Changed validation failure messages from `qDebug` to `qCritical` for better visibility without debug mode.
- **Deploy Manager**: Added version display (v2.3.2 format) in status bar center for quick reference during deployments.

[Changed]
- **Versioning**: Standardized version format across all components to use 3-part semantic versioning (major.minor.patch), dropping the fourth build number from user-facing displays.

---

## 2026-01-14 - v2.3.2.98

[Internal]
- **Build**: Internal build / Version increment skipped in git history.

---

## 2026-01-14 - v2.3.2.97

[Fixed]
- **Banner**: Adjusted bottom margin for top-docked banner to prevent overlap with maximized applications.
- **Banner**: Fixed right text alignment issue where characters were truncated.
- **Build**: Fixed CMake configuration for SmartCard Manager path.

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
