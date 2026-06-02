# BlockADS

Bộ lọc AdGuard cá nhân — chặn popup OAuth tự bật, ad networks bẩn, scam domain.

## Subscribe

Trong **AdGuard** (Mac / Windows / iOS / Android):
`Settings` → `Filters` → `Custom filters` → `Add custom filter` → paste URL:

```
https://cdn.jsdelivr.net/gh/Khoaamz/BlockADS@main/blocklist.txt
```

Hoặc raw GitHub (chậm hơn, có rate limit):

```
https://raw.githubusercontent.com/Khoaamz/BlockADS/main/blocklist.txt
```

AdGuard sẽ tự refresh hàng ngày theo header `Expires: 1 day`.

## Nội dung

| Section | Phạm vi |
|---|---|
| `luottruyen*` | Chặn popup OAuth Google ép bật trên site lô đề `luottruyen[1-99].*` |
| `Mobile ad networks` | Chặn popup, push notif, crypto miner, URL shortener bẩn |
| `Element hiding` | Ẩn floating button Telegram/Zalo, sticky banner, app banner |

## Chiến lược chặn (7 tầng)

1. **OAuth `client_id`** — chặn theo Google Cloud Project ID (chống đổi domain)
2. **`redirect_uri` keyword** — bắt khi đổi client nhưng giữ pattern tên
3. **Wildcard domain** — `||luottruyen*^`
4. **`$popup` modifier** — chặn popup window do site tự mở
5. **Cụ thể domain hiện tại**
6. **Scriptlet** — vô hiệu hoá `window.open` + Google Identity API
7. **CSS hiding** — ẩn iframe + modal đăng nhập

## Thêm domain mới

Mở `blocklist.txt`, copy template SECTION ở cuối file:

```
! ##########################################################
! # SECTION: <tên-site> (<lý do>)
! # Added: <YYYY-MM-DD>
! ##########################################################

||<domain>.com^$popup
```

Commit + push → AdGuard tự pull bản mới trong vòng 24h.

## License

MIT
