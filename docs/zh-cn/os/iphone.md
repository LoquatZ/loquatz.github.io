## iPhone 关闭系统升级

将下面命令复制到剪切板，然后使用 Filza 找到 /usr/bin/vm_stat 点击运行，然后粘贴下面命令并回车运行

```bash
killall -9 softwareupdateservicesd & killall -9 softwareupdated & killall -9 com.apple.MobileSoftwareUpdate.CleanupPreparePathService & killall -9 Preferences & chflags -R noschg,noschange,nosimmutable '/var/MobileSoftwareUpdate/MobileAsset/' & mkdir -p '/var/MobileSoftwareUpdate/MobileAsset/AssetsV2/' && rm -rf '/var/MobileSoftwareUpdate/MobileAsset/AssetsV2/' && mkdir -p '/var/MobileSoftwareUpdate/MobileAsset/AssetsV2/' && chmod -R 0777 '/var/MobileSoftwareUpdate/MobileAsset/AssetsV2/' && chown -R mobile:mobile '/var/MobileSoftwareUpdate/MobileAsset/AssetsV2/' && chflags schg,schange,simmutable '/var/MobileSoftwareUpdate/MobileAsset/AssetsV2/'
```

后续重新启用请在 Filza 运行下面的命令

```bash
chflags -R noschg,noschange,nosimmutable '/var/MobileSoftwareUpdate/MobileAsset/'
```