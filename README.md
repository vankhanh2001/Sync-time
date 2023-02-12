
    
    wget --no-check-certificate "https://raw.githubusercontent.com/thangnguyencl/Sync-time-/main/times-openwrt" -O /usr/bin/times-openwrt && chmod +x /usr/bin/times-openwrt
    
    
    
 - dùng curl:
    
    ```
    curl -sL https://raw.githubusercontent.com/thangnguyencl/Sync-time-/main/times-openwrt > /usr/bin/times-openwrt && chmod +x /usr/bin/times-openwrt
    ```


    ```
    /usr/bin/times-openwrt m.tv360.vn
    ```


    ```
    0 * * * * /usr/bin/times-openwrt m.tv360.vn cron
    ```

    
