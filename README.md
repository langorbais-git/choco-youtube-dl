"# choco-youtube-dl" 
1. install chocolate on your computer
--- 1. open powershell using 'RUN AS ADMINISTRATOR'
--- 2. Paste the 'follow' and 'run'

$securityProtocolSettingsOriginal = [System.Net.ServicePointManager]::SecurityProtocol

try {
  # This should work in .NET 4 where .NET 4.5 is installed as an inplace upgrade
  # Set TLS1.2 (3072) then TLS1.1 (768), then TLS 1.0 (192), finally SSL3 (48)
  $securityProtocolSettings = 3072 -bor 768 -bor 192 -bor 48 
  [System.Net.ServicePointManager]::SecurityProtocol = $securityProtocolSettings
} catch {
  Write-Warning "Unable to set PowerShell to use TLS 1.2 and TLS 1.1 due to old .NET Framework installed. Please upgrade to at least .NET Framework 4.5 and PowerShell v3 for this to work appropriately."
}

iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

[System.Net.ServicePointManager]::SecurityProtocol = $securityProtocolSettingsOriginal


--- 3. Close and Reopen powershell

2. install youtube-dl using choco
--- 1. choco install youtube-dl
--- 2. enter 'a' and press enter for any prompts
--- 3. choco install ffmpeg
--- 4. enter 'a' and press enter for any prompts

3. open 'cmd' and use 'youtube-dl'
--- 1. to download a single video
------>  youtube-dl -ciw -f mp4 https://www.youtube.com/watch?v=dQw4w9WgXcQ -o "%(title)s.%(ext)s"
--- 2. to download a playlist
------>  youtube-dl -ciw -f mp4 https://www.youtube.com/playlist?list=PLv3TTBr1W_9tppikBxAE_G6qjWdBljBHJ -o "%(playlist_index)s %(title)s.%(ext)s"
--- 3. to extract audio from video
------>  youtube-dl -ciw --extract-audio --audio-format mp3 --audio-quality 0 https://www.youtube.com/watch?v=dQw4w9WgXcQ -o "%(title)s.%(ext)s"
--- 4. to Download Youtube videos with subtitles
------>  youtube-dl --write-auto-sub https://www.youtube.com/watch?v=VN0XWMo3ugY
--- 5. to download with specific subtitle
------>  youtube-dl --write-srt --sub-lang en https://www.youtube.com/watch?v=VN0XWMo3ugY
--- 6. to download with multiple subtitle langage
------>  youtube-dl --write-srt --sub-lang "en,fr" https://www.youtube.com/watch?v=VN0XWMo3ugY
--- 7. to Download Youtube videos without subtitles
------>  youtube-dl https://www.youtube.com/watch?v=VN0XWMo3ugY
