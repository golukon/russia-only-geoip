# Что это?

Этот проект каждый день в 00:00 UTC автоматически генерирует `geoip.dat` с российскими IPv4 для прокси/VPN-приложений (Xray, V2Ray и др.). Таким образом, маршрут по умолчанию должен быть `proxy`, совпадение с адресом из файла — `direct`. Файл получается небольшим (около `90 Кб`, удобен для роутеров), также отпадает необходимость постоянно включать/выключать VPN.

Источник данных: [iwik.org](https://iwik.org/ipcountry)

### Содержимое geoip.dat

- `geoip:ru` — список всех российских IPv4-адресов
- `geoip:private` — приватные и зарезервированные сети, например `10.0.0.0/8`, `127.0.0.0/8`, `192.168.0.0/16`

## Смежные проекты

- [@golukon/russia-only-geosite](https://github.com/golukon/russia-only-geosite) — файл `geosite.dat` с сайтами, доступ к которым разрешён внутри России
- [@golukon/russia-v2ray-rules-lite](https://github.com/golukon/russia-v2ray-rules-lite) — репозиторий со всеми geo файлами для xray и sing-box

## Пример конфигурации для v2rayA (совместно с geosite.dat)

```
default: proxy
ip(geoip:private)->direct

# write your own rules below
ip(geoip:ru)->direct
domain(geosite:ru-inside)->direct
```

## Пример конфигурации для v2rayN/v2rayNG (совместно с geosite.dat)

```
[
    {
        "enabled": true,
        "ip": [
            "geoip:private"
        ],
        "locked": false,
        "outboundTag": "direct",
        "remarks": "RU-0 [Приватные сети напрямую]"
    },
    {
        "enabled": true,
        "ip": [
            "geoip:ru"
        ],
        "locked": false,
        "outboundTag": "direct",
        "remarks": "RU-0 [Российские IPv4 напрямую]"
    },
    {
        "domain": [
            "geosite:ru-inside"
        ],
        "enabled": true,
        "locked": false,
        "outboundTag": "direct",
        "remarks": "RU-0 [Российские домены напрямую]"
    },
    {
        "enabled": true,
        "locked": false,
        "outboundTag": "proxy",
        "port": "0-65535",
        "remarks": "RU-0 [Остальное прокси]"
    }
]
```

## Скачать

По ссылкам ниже всегда доступна последняя версия файлов.

- **github**
    - [https://raw.githubusercontent.com/golukon/russia-only-geoip/release/geoip.dat](https://raw.githubusercontent.com/golukon/russia-only-geoip/release/geoip.dat)
    - Hashsum: [https://raw.githubusercontent.com/golukon/russia-only-geoip/release/geoip.dat.sha256sum](https://raw.githubusercontent.com/golukon/russia-only-geoip/release/geoip.dat.sha256sum)
- **JSDelivr**
    - [https://cdn.jsdelivr.net/gh/golukon/russia-only-geoip@release/geoip.dat](https://cdn.jsdelivr.net/gh/golukon/russia-only-geoip@release/geoip.dat)
    - Hashsum: [https://cdn.jsdelivr.net/gh/golukon/russia-only-geoip@release/geoip.dat.sha256sum](https://cdn.jsdelivr.net/gh/golukon/russia-only-geoip@release/geoip.dat.sha256sum)
- **Fastly + JSDelivr**
    - [https://fastly.jsdelivr.net/gh/golukon/russia-only-geoip@release/geoip.dat](https://fastly.jsdelivr.net/gh/golukon/russia-only-geoip@release/geoip.dat)
    - Hashsum: [https://fastly.jsdelivr.net/gh/golukon/russia-only-geoip@release/geoip.dat.sha256sum](https://fastly.jsdelivr.net/gh/golukon/russia-only-geoip@release/geoip.dat.sha256sum)

## Благодарности

- [@Loyalsoldier/geoip](https://github.com/Loyalsoldier/geoip) — сборщик geoip.dat
- [@runetfreedom/russia-blocked-geoip](https://github.com/runetfreedom/russia-blocked-geoip) — шаблон репозитория
- [scanitex.com](https://scanitex.com/ru/resources/ip-ranges/ru) — список российских ip адресов
