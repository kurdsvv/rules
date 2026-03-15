1.排序节点
```
awk -F, -v OFS=',' '!seen[$2 FS $3]++' file.csv > output.csv
```

2.格式化日志
```
awk -F. '{if (NF>=2) print $(NF-1)"."$NF}' domains.txt | sort | uniq -c | sort -nr
 
awk -F'"QH":' '{print $2}' data.txt | awk -F'"' '{print $2}'
```

3.排序域名
```powershell
awk -F'[.]' '
{
    if (NF > 2) {
        # 有二级域名的行，提取主域名
        main_domain = $(NF-1) "." $NF;
        has_subdomains[main_domain] = has_subdomains[main_domain] "\n" $0;
    } else {
        # 没有二级域名的行
        no_subdomains = no_subdomains "\n" $0;
    }
}
END {
    # 输出有二级域名的分组
    for (d in has_subdomains) {
        print has_subdomains[d];
    }
    # 输出没有二级域名的部分
    if (no_subdomains) {
        print no_subdomains;
    }
}
' input.txt > output.txt
```
4.合并文件夹所有ts
```
cd C:\path\to\ts_files

Get-ChildItem *.ts |
Sort-Object {
    if ($_.BaseName -match '_(\d+)$') {
        [int]$matches[1]
    } else {
        -1
    }
} |
ForEach-Object {
    "file '$($_.Name)'"
} | Set-Content filelist.txt -Encoding UTF8



ffmpeg -f concat -safe 0 -i filelist.txt -c copy output.mp4
```
5.Clash-verge格式存储
```
    - {name:

      - 
```
6.🔒 锁这个文件
```
icacls "%APPDATA%\Telegram Desktop\Updater.exe" /deny %USERNAME%:(F)

icacls "%APPDATA%\Telegram Desktop\Updater.exe" /remove:d %USERNAME%
```
7.🔒 锁这个目录
```
icacls "%APPDATA%\Telegram Desktop" /inheritance:r

icacls "%APPDATA%\Telegram Desktop" /grant Users:(OI)(CI)RX

icacls "%APPDATA%\Telegram Desktop" /deny Users:(OI)(CI)(W,WD,AD,DC)

icacls "%APPDATA%\Telegram Desktop" /remove:d Users
```
8.转录文件
```
for %i in (*.webm) do ffmpeg -i "%i"  -c:v h264_nvenc "%~ni.mp4"
```
9.ECH 域名
```
crypto.cloudflare.com
cloudflare-ech.com
```


crypto.cloudflare.com
