1.  **Initialize Git Repository (in an empty directory)**:
    *   Command: `git init`
    *   Explanation: Initializes an empty Git repository in the Linux_kernel directory.

2.  **Add Kernel.org Remote**:
    *   Command: `git remote add origin https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git`
    *   Explanation: Adds the official Linux kernel repository (Linus Torvalds' tree) as a remote named 'origin'.

3.  **Fetch Kernel Source Code**:
    *   Command: `git fetch origin`
    *   Explanation: Downloads all branches and tags from the 'origin' remote.

4.  **Checkout Master Branch**:
    *   Command: `git checkout master`
    *   Explanation: Switches to the local 'master' branch.

5.  **Reset Local Master to Remote**:
    *   Command: `git reset --hard origin/master`
    *   Explanation: Resets the local 'master' branch to exactly match the state of the 'origin/master' branch, ensuring the latest code is checked out and no accidental or intentional modifications are present before compilation.

6.  **Configure the Kernel**:
    *   Action: You ran `make defconfig`.
    *   Explanation: This creates a default kernel configuration file (`.config`) tailored for the system's architecture.

7.  **Compile the Kernel**:
    *   Action: You ran `make` (likely with a `-j` option for parallel compilation).
    *   Explanation: This compiles the kernel source code based on the `.config` file. This step is successful after installing the missing dependency.

7.1.  **Compile may fail due to lack of dependecy (like mine did)**:
    *   Action: You installed `libelf-dev` (or its equivalent for your distribution).
    *   Explanation: This was done to resolve the `fatal error: gelf.h: No such file or directory` encountered during the first compilation attempt.

8.  **Install Kernel Modules**:
    *   Command: `sudo make modules_install`
    *   Explanation: This command installs all the compiled kernel modules into the appropriate directory under modules. This needs to be run from your kernel source directory (Linux_kernel).

9.  **Install the Kernel**:
    *   Command: `sudo make install`
    *   Explanation: This command copies the compiled kernel (`vmlinuz` or similar) and the `System.map` file to your boot directory. It will also try to update your bootloader configuration (e.g., GRUB). This also needs to be run from your kernel source directory.

10.  **Update Bootloader (if not done automatically by `make install`)**:
    *   Explanation: The `make install` command often handles this, but if it doesn't, or if you want to be sure, you might need to manually update your bootloader configuration. The command depends on your bootloader (most commonly GRUB).
    *   For GRUB (common on many systems): `sudo update-grub` or `sudo grub-mkconfig -o /boot/grub/grub.cfg` (the exact command can vary slightly depending on your distribution).

11.  **Reboot Your System**:
    *   Command: `sudo reboot`
    *   Explanation: After the kernel and modules are installed and the bootloader is updated, you'll need to reboot your system. When the bootloader menu appears, you should see an option for your new kernel. Select it to boot into your custom-compiled kernel.

**Important Considerations:**

*   **Backup**: Before installing a new kernel, especially if it's your first time, it's wise to back up any important data.
*   **Old Kernel**: Your old kernel should still be available in the bootloader menu. If the new kernel has problems, you can reboot and select your old, working kernel.
*   **Disk Space**: Ensure you have enough space in your boot partition for the new kernel files.

Please proceed with these steps carefully. Let me know if you want me to execute any of these commands for you or if you have questions about any step.