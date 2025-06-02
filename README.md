# lab2-group-policy-management
Use Group Policy Objects (GPOs) to control user and computer settings centrally in a Windows domain environment.
# 🧪 Lab 2: Group Policy Management

## Objective
Learn to centrally manage user and computer settings using Group Policy Objects (GPOs) in a Windows domain environment.

---

## Lab Environment
- **Domain Controller**: Windows Server 2016
- **Client VM**: Windows 10 (joined to domain)
- **Test User/Computer**: Placed in a custom Organizational Unit (Lab 2 Users)

---

## Tasks Performed

### 1. Created and Linked a GPO
- Created an Organizational Unit (OU) named `Lab2Users`
- Moved a test user and/or computer into the OU
- Created and linked a new GPO called `Test GPO` to `Lab2Users`

### 2. Configured Group Policy Settings
#### ✅ User Configuration:
- **Disabled Control Panel**:  
  `User Configuration > Policies > Administrative Templates > Control Panel > Prohibit access to Control Panel and PC settings`

- **Set Desktop Wallpaper**:  
  `User Configuration > Policies > Administrative Templates > Desktop > Desktop Wallpaper`  
  (Path used: `\\Server01\shared\asap.rocker.jpg`)

#### ✅ Computer Configuration:
- **Password Policy** (applied via Default Domain Policy):  
  `Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy`  
  (e.g., min. password length: 8, complexity enabled)

---

## 🧪 Testing
On the client VM:

- Logged in using the test user account.
- Ran `gpupdate /force` in Command Prompt.

**Results:**

- Control Panel was successfully disabled — I got a restriction message when I tried to open it.
- The wallpaper was applied, though it didn’t work the first time (turns out the client couldn't access the shared folder — fixed it by adjusting share permissions).
- Password policy changes kicked in when I tried to change the user’s password — complexity was enforced as expected.

---

## 📸 Screenshots

- [GPO Creation](screenshots1/newOrganisationalUnit.png)
- [Control Panel Disabled](screenshots1/ControlPanelDisabled.png)
- [Control_Panel_Disabled2](screenshots1/ControlPanelDisabled2.png)
- [Disabled_ControlPanel_in_Server](screenshots1/implyingDisableControlPanel.png)
- [Wallpaper Applied](screenshots1/WallpaperChanged.png)
- [Wallpaper-change-setting-in-Server](screenshots1/Wallpaper-change-setting-in-server.png)
- [Password Policy](screenshots1/PasswordPolicyEnforced.png)
- 

---

## 📘 Key Takeaways

- How to create and link GPOs to OUs
- User vs Computer Configuration in GPO
- Practical impact of GPOs on domain-joined clients
- Importance of proper OU structure for policy targeting

### 💭 Reflections

This lab really helped me understand how powerful and picky GPOs can be. At first, I was confused why my settings weren’t applying — but I learned that:

- GPOs must be linked to the correct **Organizational Unit (OU)**, not just the domain.
- **Permissions and file paths** matter a lot, especially for things like wallpapers.
- There’s a clear difference between **User Configuration** and **Computer Configuration** — and getting them mixed up won’t throw errors, just silent failure.

Overall, this was a solid hands-on way to see how real sysadmins manage centralized settings. Definitely something I’ll use again in enterprise environments.

---

## ✅ Status
✔️ Lab completed successfully.
