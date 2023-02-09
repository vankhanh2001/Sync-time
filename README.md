- Đồng bộ hóa ngày openwrt bằng cách chọn ngày từ miền đã chọn.
- Đồng bộ hóa thời gian trong OpenWrt bằng cách lấy dữ liệu thời gian từ miền đã chọn.
- Hỗ trợ đồng bộ thời gian khi có kết nối modem/internet.
- Trình kiểm tra kết nối (nếu sử dụng chế độ cron, tập lệnh sẽ kiểm tra kết nối, sau đó khởi động lại ứng dụng VPN nếu không có kết nối internet)
- Cài đặt múi giờ tự động tuân theo LuCI - System - System - Timezone.
- Hỗ trợ cài đặt múi giờ cho VPN:
    - OpenClash
    - Passwall
    - ShadowsocksR
    - ShadowsocksR++
    - v2ray
    - v2rayA
    - xray
    - Libernet
    - Xderm Mini
    - Wegare STL

### Sử dụng mặc định - Sử dụng cơ bản
Cài đặt các gói yêu cầu trước bằng cách mở terminal:
    ```
    opkg update && opkg install curl wget httping
    ```

- Dán lệnh bên dưới để cài đặt tập lệnh ``time-openwrt``
- Dùng wget:

    ```
    wget --no-check-certificate "https://raw.githubusercontent.com/thangnguyencl/Sync-time-/main/time-openwrt" -O /usr/bin/time-openwrt && chmod +x /usr/bin/time-openwrt
    ```
    
 - dùng curl:
    
    ```
    curl -sL https://raw.githubusercontent.com/thangnguyencl/Sync-time-/main/sync-time-openwrt > /usr/bin/sync-time-openwrt && chmod +x /usr/bin/time-openwrt
    ```
- Nhập lệnh bên dưới vào LuCI -> System -> Startup -> Local Startup hoặc tại rc.local nếu ở trong terminal
- Ví dụ dùng mạng Viettel:

    ```
    /usr/bin/time-openwrt m.tv360.vn
    ```

- Nếu sử dụng crontab (kiểm tra kết nối cứ sau 1 giờ, sau đó khởi động lại vpn nếu không có kết nối), sao chép lệnh bên dưới vào LuCI -> System -> Schedule Tasks Ví dụ:
    ```
    0 * * * * /usr/bin/time-openwrt m.tv360.vn cron
    ```

    - Lệnh trên cũng có thể được bao gồm trong tệp/etc/crontabs/root
    - Đối với các tùy chỉnh thời gian định kỳ khác, hãy xem [crontab.guru](https://crontab.guru/#0_*_*_*_*)
    
### Advanced Usage - Pemakaian Lanjutan

- Ganti **``www.site.com ``** dengan **``bug/domain``** kesayangan anda. Contoh:

    ```
    /usr/bin/time-openwrt m.youtu.be
    ```

- Jika menggunakan **``0p0k Telkomsel``** silahkan tambahkan **``:443``** dibelakang bug. Contoh:

    ```
    /usr/bin/time-openwrt www.site.com:443
    ```

- Jika ingin melakukan **``update/pembaruan script``**, silahkan lakukan perintah dibawah ini.

    ```
    /usr/bin/time-openwrt update
    ```
    Tanda update berhasil adalah seperti ini:
    ```
    sync-time-openwrt: Updating script...
    sync-time-openwrt: Downloading script update...
    sync-time-openwrt: Update done...
    sync-time-openwrt: update file cleaned up!
    Usage: add domain/bug after script!.
    jam.sh: Missing URL/Bug/Domain!. Read https://github.com/vitoharhari/sync-date-openwrt-with-bug/blob/main/README.md for details.
    ```

### How This Script Work - Cara Kerja Script Ini
- Setelah script dimasukkan ke **``Local Startup``** atau di **``rc.local``** dengan menambahkan domain/bug/URL (maupun port)
- Device OpenWrt restart, lalu script **``memeriksa koneksi internet``** terlebih dahulu.
- Jika internet belum tersedia, script akan **``mengulangi pemeriksaan koneksi sampai koneksi terhubung``**.
- Ketika koneksi sudah terhubung, script akan **``melakukan sinkronisasi waktu``**.
- Jika ada **``aplikasi VPN/Tunneling yang berjalan``**, script akan **``merestart aplikasi VPN yang digunakan``** sebelum melakukan sinkronisasi waktu.

### Developer - Pengembang
- Base script and more enhancement codes from AlkhaNet by [Teguh Surya Mungaran](https://github.com/alkhanet26)
- GMT codes and more enhancement codes by [Vito H.S](https://github.com/vitoharhari)
- opkg checker and installer, internet checker, vpn manager, gmt selection codes by [Helmi Amirudin](https://helmiau.com)
