
---

> 环境：ubuntu

使用nptdate 时间服务器，但是时间依然没有更改。于是更改想到更改时区。

```shell
date -R 
Wed, 23 Jan 2019 06:19:08 +0000
# 修改时区
tzselect
Please identify a location so that time zone rules can be set correctly.
Please select a continent, ocean, "coord", or "TZ".
 1) Africa
 2) Americas
 3) Antarctica
 4) Asia
 5) Atlantic Ocean
 6) Australia
 7) Europe
 8) Indian Ocean
 9) Pacific Ocean
10) coord - I want to use geographical coordinates.
11) TZ - I want to specify the time zone using the Posix TZ format.
#? 4
Please select a country whose clocks agree with yours.
 1) Afghanistan           18) Israel                35) Palestine
 2) Armenia               19) Japan                 36) Philippines
 3) Azerbaijan            20) Jordan                37) Qatar
 4) Bahrain               21) Kazakhstan            38) Russia
 5) Bangladesh            22) Korea (North)         39) Saudi Arabia
 6) Bhutan                23) Korea (South)         40) Singapore
 7) Brunei                24) Kuwait                41) Sri Lanka
 8) Cambodia              25) Kyrgyzstan            42) Syria
 9) China                 26) Laos                  43) Taiwan
10) Cyprus                27) Lebanon               44) Tajikistan
11) East Timor            28) Macau                 45) Thailand
12) Georgia               29) Malaysia              46) Turkmenistan
13) Hong Kong             30) Mongolia              47) United Arab Emirates
14) India                 31) Myanmar (Burma)       48) Uzbekistan
15) Indonesia             32) Nepal                 49) Vietnam
16) Iran                  33) Oman                  50) Yemen
17) Iraq                  34) Pakistan
#? 9
Please select one of the following time zone regions.
1) Beijing Time
2) Xinjiang Time
#? 1

# 然后从查看，时区依然没有更改，
sudo cp /usr/share/zoneinfo/Asia/Shanghai  /etc/localtime 
date -R
Wed, 23 Jan 2019 14:19:53 +0800
# 更改成功

sudo hwclock  -w   # 写入bios  ，重启不失效
```

**bug**：用上面更改时间的方法，java程序无法读出系统的正确时间

用亚马逊提供的修改时间的方法[chrony ](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/set-time.html )也不行。
 
但用 :` sudo dpkg-reconfigure tzdata` 就可以
 `sudo dpkg-reconfigure locales`  扩展一下，修改语言
 


