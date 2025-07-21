This repository contains PowerShell scripts designed for use as remediation scripts in Microsoft Intune. The scripts automate the detection and updating of outdated Chocolatey packages on Windows devices.

## Scripts

### chocoUpdateAllDetect.ps1

**Purpose:**  
Detects if any Chocolatey packages are outdated on the device.

**How it works:**

- Checks if Chocolatey is installed; installs it if missing.
- Runs `choco outdated` to list outdated packages.
- If any outdated packages are found, the script writes a message and exits with code 1 (indicating remediation is needed).
- If all packages are up to date, it writes a message and exits with code 0.

**Usage:**  
Assign this script as a detection script in Intune Remediations to determine if remediation (updating) is required.

---

### chocoUpdateAllRemediate.ps1

**Purpose:**  
Updates all outdated Chocolatey packages on the device.

**How it works:**

- Checks if Chocolatey is installed; installs it if missing.
- Runs `choco outdated` and parses the output to get the list of outdated packages.
- Attempts to upgrade each outdated package using `choco upgrade`.
- Logs the result of each upgrade attempt.

**Usage:**  
Assign this script as a remediation script in Intune Remediations to automatically update outdated Chocolatey packages.

---

## How to Use in Intune

These scripts are intended to be used with the **Devices > Scripts and remediations** feature in Microsoft Intune.

1. **Go to the Microsoft Intune admin center.**
2. Navigate to **Devices** > **Scripts and remediations**.
3. Click **Create script package**.
4. In the **Basics** section, provide a name and description for the remediation.
5. In the **Detection script** section, upload the `chocoUpdateAllDetect.ps1` script.
6. In the **Remediation script** section, upload the `chocoUpdateAllRemediate.ps1` script.

**On the page where you add the detection and remediation scripts, use these settings:**

- **Run this script using the logged-on credentials:** No
- **Enforce script signature check:** No
- **Run script in 64-bit PowerShell:** Yes

7. Assign the script package to the desired Azure AD device group.
8. Review and create the remediation assignment.

This setup ensures that devices with outdated Chocolatey packages are automatically detected and remediated

---

## License

- This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
