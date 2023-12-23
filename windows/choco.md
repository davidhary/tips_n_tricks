Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

choco install -y firefox 7zip notepadplusplus totalcommander googlechrome mremoteng thunderbird putty mpc-hc-clsid2 foobar2000 winscp qbittorrent teamviewer anydesk javaruntime win32diskimager keepass lightshot msiafterburner steam
