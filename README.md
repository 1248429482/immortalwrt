# 自用高通版 ImmortalWRT
高通部分源码取自以下项目：

https://github.com/JiaY-shi/openwrt.git

https://github.com/qosmio/openwrt-ipq.git

https://github.com/LiBwrt-op/openwrt-6.x.git

https://github.com/King-Of-Knights/openwrt-6.x.git



sudo bash -c 'bash <(curl -s https://build-scripts.immortalwrt.org/init_build_environment.sh)'
git clone https://github.com/VIKINGYFY/immortalwrt.git
cd immortalwrt
./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig
make


ImmortalWrt 23.05.4 released

- Core components update

   - hostapd: fix SAE H2E security vulnerability
   - kernel: backport bpf_loop support, update to 5.15.167
   - mac80211: fix wifi throughput, update to 6.1.110
   - mbedtls: update to 2.28.9
   - openssl: update to 3.0.15

- Targets update

   - ath79
      - fix I2C pins on GL-AR750
      - fix PHY mii settings

   - ipq40xx
      - fix PHY mii settings
      - improve compatibility with newer Aruba apboot revs

   - mediatek
      - add support for several new devices
         - CMCC A10 (OpenWrt U-Boot layout)
         - Imou LC-HX3001 (OpenWrt U-Boot layout)
         - Konka KOMI A31
      - add PHY LED configuration for Zyxel EX5700
      - fix PHY reset for JDCloud RE-CP-03

   - ramips
      - add support for OpenFi 5Pro
      - enable lzma-loader for Sercomm NA502s
      - fix PHY MII settings

   - realtek
      - backport VLAN fix

   - rockchip
      - add support for several new devices
         - ArmSoM Sige3
         - LYT T68M
      - backport upstream fixes for FastRhino R66S/R68S
      - enable wifi and bt for Firefly Station P2

   - x86
      - include Intel DMC firmware by default
      - include Realtek 5GbE PCIe Network Adapter driver by default

... with other bug fixes and performance improvements :D

Get firmware at:
https://firmware-selector.immortalwrt.org/?version=23.05.4
https://downloads.immortalwrt.org/releases/23.05.4/targets/
https://mirrors.ustc.edu.cn/immortalwrt/releases/23.05.4/targets/

Setup opkg mirror (live in mainland China):
https://help.mirrorz.org/immortalwrt/

Revert to main opkg feed (not in mainland China):
sed -i.bak "s,mirrors.vsean.net/openwrt,downloads.immortalwrt.org,g" "/etc/opkg/distfeeds.conf"

We have introduced a new option in system configuration to persist mirror setting, e.g.:
uci set system.@imm_init[0].opkg_mirror='https://mirrors.vsean.net/openwrt'
uci commit system

⚠️ For x86 users, run opkg upgrade luci-app-attendedsysupgrade and clean browser cache first if you want to use Attended Sysupgrade feature.
