# :sun_with_face: Awesome Security Tool List & Useful Commands :four_leaf_clover:

This is a list of security tools & commands that I have used or recommend. I'm using Kali Linux. Welcome any contributions! :muscle:

& Wish you all good luck on your way of finding the hidden treasures. :wink:

## Table of Contents

:gem: **[Software Tools](#sun_with_face-software-tools)**

:gem: **[Common Commands & CLI](#sun_with_face-common-commands--cli)**

:gem: **[Learning / Practicing Websites](#sun_with_face-learning--practicing-websites)**

:gem: **[Special Thanks](#sun_with_face-special-thanks)**

## :sun_with_face: Software Tools

1. **[Ghidra](https://ghidra-sre.org/): Decompile binary files.**
   - Satisfy the [minimum requirements](https://ghidra-sre.org/InstallationGuide.html#Requirements) (Java 11 JDK) and download Ghidra from the above website.
   - After extracting the downloaded Ghidra package, open `ghidraRun.bat` to start.
   - Select New project > Import Files, then select your binary file to analyze.
   - In the `Symbol Tree` tab on the left, find and select `main` under `Functions`.
   - Then, select `Windows` > `Decompile:main` from the top menu to see readable code.
2. **[StegSolve](https://github.com/zardus/ctf-tools/blob/master/stegsolve/install): A java app that solves steganography by apply various filters.**
   - Steganography is to conceal a message, image, or file within another message, image, or file.
   - Installation instruction is in the above link.
   - Reference: [Wiki](https://en.wikipedia.org/wiki/Steganography)
3. **[Burp Suite Professional](https://portswigger.net/burp/pro): A software that uses proxy (usually localhost:8080) to intercept HTTP requests.**
   - You can edit and resend the intercepted HTTP requests.
   - The Community version is very slow.. don't use it. You should be able to find free professional licenses online:)
4. **[IDA Pro 32/64 bit](https://www.hex-rays.com/products/ida/support/download_freeware/): A software that generates assembly code from binary files.**
   - Download IDA Pro 64-bit from the above link, and download IDA Pro 32-bit with pseudocode decompiler [here](https://drive.google.com/open?id=1CCRnlhXZCUwH1P5WisLf6CQtHv6dTtFZ).
   - Hotkeys:
     - `F5`: view pseudocode
     - `tab`: toggle between the disassembly code view and pseudocode view.
     - `Shift+F12`: view all strings in the program.
   - Note that 32-bit programs need to be opened with IDA Pro 32-bit, and vice versa.
   - Reference: [IDA Pro Hotkey Cheatsheet](https://www.hex-rays.com/products/ida/support/freefiles/IDA_Pro_Shortcuts.pdf)

## :sun_with_face: Common Commands & CLI

1. **`lsof -i -P -n | grep LISTEN`: Show listening ports.**
   - lsof: list open files and processes that opened them.
   - `-i`: list all network connections.
   - `-P`: list port number instead of port name.
   - `-n`: don't convert network number to hostname, this can make lsof run faster.
   - reference: [manual](https://man7.org/linux/man-pages/man8/lsof.8.html)
2. **`xdg-open .`: Open current folder in GUI explorer.**
   - This is useful for drag and drop files from Linux VM to host computer.
   - reference: [StackExchange](https://askubuntu.com/questions/31069/how-to-open-a-file-manager-of-the-current-directory-in-the-terminal)
3. **`kill $(lsof -t -i:8080)`: Kill any process listening on port 8080.**
   - reference: [StackOverflow](https://stackoverflow.com/questions/11583562/how-to-kill-a-process-running-on-particular-port-in-linux)
4. **`display <image_name>`: Display image from terminal.**
   - Make sure that [imagemagick](https://tecadmin.net/install-imagemagick-on-linux/) is installed before using this.
   - reference: [StackExchange](https://unix.stackexchange.com/questions/35333/what-is-the-fastest-way-to-view-images-from-the-terminal)
5. **`nc -l -p 9000`: Listen on port 9000**
   - use `nc <ip_address> 9000` to communicate with the host.
6. **`grep -rnw '/path/to/somewhere/' -e 'pattern'`: Find all files containing the pattern under the specified path.**
   - `-r`: recursively search
   - `-n`: display the line number containing the pattern in the file.
   - `-w`: match the entire word of the pattern.
   - Reference: [StackOverflow](https://stackoverflow.com/questions/16956810/how-do-i-find-all-files-containing-specific-text-on-linux)
7. **`strings <filename>`: Print all strings in the file.**
   - use `strings <filename> | grep -E <some_regex>` to find the strings that matches the regular expression, `FLAG{[a-zA-Z0-9_!@]+}`, for example.
   - Test regular expressions online at https://regexr.com/.
8. **`strace <filename>`: Print out system call details.**
   - If not installed, run `sudo apt-get install strace`.
   - Use `strace -s 50 <filename>` to print out the strings with max length 50.
   - Reference: [manual](https://man7.org/linux/man-pages/man1/strace.1.html)
9. **`objdump -M intel -d <filename> | less`: Show the disassembled file.**
   - `-M intel`: display the assembly in Intel syntax (see the differences between the default AT&T syntax and the Intel syntax in [wiki](https://en.wikipedia.org/wiki/X86_assembly_language#Syntax)).
   - `-d`: disassemble
   - `-C`: decode (demangle) low-level symbol names into readable names
   - The `less` command is for viewing the contents of the file, allow both forward and backward navigation. (The `more` command only allow forward navigation.)
   - Can also use `grep` to get specific data.
   - When using `less` to view the file, you can use `/<anything_you_want_to_search>` to search for specific strings. For example, use `/main` to locate the main function.
   - Reference: [manual](https://sourceware.org/binutils/docs/binutils/objdump.html)
10. **`binwalk -Mre <filename>`: Firmware analysis & reverse engineering.**

    - Follow the installation instructions [here](https://github.com/ReFirmLabs/binwalk/blob/master/INSTALL.md).

    - `-M`: recursively scan extracted files.
    - `-r`: delete carved file after extraction. ([what is file carving?](https://resources.infosecinstitute.com/file-carving/#gref))
    - `-e`: extract known file types.
    - Reference: [Github](https://github.com/ReFirmLabs/binwalk)

11. **`qemu-mipsel <filename>`: Execute MIPS programs on non-MIPS OS.**

    - [Installation instructions](https://zoomadmin.com/HowToInstall/UbuntuPackage/qemu-system-mips)
    - If you run into "No such file or directory", run `export QEMU_LD_PREFIX=<folder_location_of_the_missing_file>` and retry the above command to help the program find your file.
    - QEMU: Quick EMUlator
    - mipsel: little-endian MIPS / mips: big-endian MIPS ([little vs big endian?](https://chortle.ccsu.edu/AssemblyTutorial/Chapter-15/ass15_3.html))
    - Reference: [Official Website](https://www.qemu.org/docs/master/system/target-mips.html)

12. **`gdb ./<executable_program>`: The GNU Project Debugger.**
    - Install: `sudo apt-get update` then `sudo apt-get install gdb`.
    - Common commands in the gdb console:
      - `r`: run the program until next breakpoint or error
      - `c`: continue running the program
      - `f`: run the program until current function is finished
      - `s`: step to the next line of the program
        `n`: step to the next line of the program, but does not step into functions
      - `b main`: set breakpoint at the main function
      - `d`: delete all breakpoints
      - `jump *main+135`: jump to the address of the main function address with offset 135
      - `p/x $rax`: print the rax register in hex
      - `p/d <variable>`: print the variable as signed integer
      - `x/wx $esp`: print the memory address of the register esp in hex format
      - `set $esi = 0x1`: set value of the register
      - `q`: quit gdb
    - Tips: Keep an eye on the `cmp` (compare) statement when looking at the assembly code, cause usually if you can pass the compare statement, you can guess the correct input of the program.
      - To bypass `cmp` statements, you can either modify the register value to the desired one or jump to the next memory address right after the `cmp` statement.
    - Reference: [Official Website](https://www.gnu.org/software/gdb/)
13. **`nc <ip> <port>`: Connect to remote server**
    - nc stands for [Netcat](https://en.wikipedia.org/wiki/Netcat)
    - Use `ncat -vc $binary -kl $ip $port` to host the binary file on a remote server.
14. **`checksec ./<executable_binary>`: Check the security properties of a program**

    - Properties checked:
      - **`Arch`: The architecture of the program.**
        - For example, `amd64-64-little` means AMD64 architecture that uses little endian.
      - **`RELRO`: Is partial or full binary sections read-only?**
        - RELRO: [Relocation Read-Only](https://ctf101.org/binary-exploitation/relocation-read-only/)
        - If full, "GOT([Global Offset Table](https://en.wikipedia.org/wiki/Global_Offset_Table)) overwrite" attack is not possible.
      - **`STACK`: Does stack canary exist?**
        - It is a technique to detect stack overflow by placing a number (named canary) before the stack return pointer, and check if the value has been changed.
        - Reference: [CTF Wiki](https://ctf-wiki.github.io/ctf-wiki/pwn/linux/mitigation/canary/)
      - **`NX`: Is NX protection enabled?**
        - NX: [No-Execute](https://ctf101.org/binary-exploitation/no-execute/)
        - If yes, we cannot use stack overflow to execute our customized shellcodes.
      - **`PIE`: Prevents attackers by randomizing the memory address of the executable.**
        - PIE: [Position Independent Executable](https://en.wikipedia.org/wiki/Position-independent_code#Position-independent_executables)
        - If enabled, we won't know the memory address until we run the program. However, we can still disable ASLR ([Address Space Layout Randomization](https://en.wikipedia.org/wiki/Address_space_layout_randomization)) on our OS to let the addresses remain the same.
        - How to disable ASLR on Linux: [StackOverflow](https://askubuntu.com/questions/318315/how-can-i-temporarily-disable-aslr-address-space-layout-randomization)
    - Reference: [Github](https://github.com/slimm609/checksec.sh)

## :sun_with_face: Learning / Practicing Websites

1. **[PortSwigger](https://portswigger.net/web-security/all-labs)**: Its web security lab covers topics across SQL injection, Cross-site scripting, Cross-site request forgery (CSRF), Cross-origin resource sharing (CORS), Server-side request forgery (SSRF), etc.
2. **[OWASP Juice Shop](https://owasp.org/www-project-juice-shop/)**: An insecure web application for you to attack! ([reference solutions](https://bkimminich.gitbooks.io/pwning-owasp-juice-shop/content/appendix/solutions.html))

## :sun_with_face: Special Thanks

- Cute emojis from [here](https://gist.github.com/rxaviers/7360908)! :blush:
