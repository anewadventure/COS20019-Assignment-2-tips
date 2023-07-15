# Assignment 2 tips

# 1. The annoying permission of SSH key files on Microsoft Windows

Microsoft Windows' file system is incompatible with the Linux file system. The permission system of Windows is Active Directory, while Linux is POSIX. You will usually get into problems like invalid permissions when using PEM key files to `ssh` over remote Linux hosts. This also happens if you use PUTTY to convert the PEM key file into PPK. It's sad that this inconvenience is still there, but there's a convenient way to work around this:

* Right-click the PEM key file and click Properties. Go to the Security tab and click Advanced permissions.
* Modify the permissions panel so that:
    * The owner of the file is you.
    * Inheritance is disabled. When you disable inheritance, a window will pop up asking whether to remove all inherited permissions or convert them to all explicit permissions. Select the option to remove.
    * Remove all other permissions presented in the panel. Add an entry that grants you Full control to that file.

If you intend to use PUTTY and WinSCP instead of the built-in OpenSSH on Windows, don't convert the PEM key file into PPK. Download the PPK key file provided in the AWS Console instead.

# 2. Choices of workflow for this assignment

* WinSCP + PUTTY: This combination is OK. The drawback is that if you want to edit sudo-protected files, you'll have to remove the key file from the setup, enable root SSH, and set up the password for the root account.

* VSCode with the Remote-SSH and Save as Root extensions: This combination is among the best one I know of. You can define the ssh hosts in the ssh configuration file, and include the file path to the PEM key file (without having to use the PPK key file). You can use Save as Root if you want to edit sudo-protected file, and because we already provided the key file, you don't need any authentication. The drawback is that this setup doesn't have the convenience of a file explorer like WinSCP, and everytime you switch to another folder (basically changing workspace folder) it will reload the window, reauthenticate and load the extensions again, which I find quite unnecessary.

* Pure SSH with Vim or Nano: This requires the least effort to set up. Vim and Nano are included by default in POSIX installations. The drawback is that there is still some problems with Microsoft's implementation of SSH, so there'll be a problem if you try to paste through an SSH'd Vim. Nano has no problem though.

