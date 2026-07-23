# Link Hub — goldenstonegames.com

Goldenstone Games'in "tüm linkler tek sayfada" sitesi. Bio'lardaki tek link alanlarına bu URL konur.

## Yapı
- `index.html` (self-contained, harici bağımlılık yok) + `avatar.png` (480px; orijinal `D:\UnrealProjects\marketing\brand\pp-original.png`) + `fonts\` (Oxanium/Necropunk, Metamorphous/Timberheim — kaynak: `D:\htmlprojects\stream-console\public\assets\fonts\`) + `icons\` (marka logoları, simple-icons SVG, fill=marka rengi gömülü; koyu zeminde X ve TikTok beyaz).
- **Public repo:** `BYGGOLDENSTONE/BYGGOLDENSTONE.github.io` — GitHub Pages, master branch kökü. Push sonrası ~1-2 dk'da canlıya geçer.
- Favicon = `avatar.png` (2026-07-23'te emoji kılıçtan değiştirildi).
- Tüm dış linkler `target="_blank" rel="noopener"` (kullanıcı isteği).

## Düzen (2026-07-23 redesign)
- **Masaüstü (>920px): 3 sütun** — Socials | Live Development (Turkish) | Games. Amaç: 1080p'de kaydırmasız tek ekran. Dar ekranda tek sütuna düşer.
- Sosyal linkler ikonlu satır; **oyun kartları İKONSUZ** — sadece oyun adı kendi tema fontuyla, tipografi odaklı (kullanıcı kararı: emoji ikon YASAK).

## Sayfa temaları (hover ile tam sayfa tema değişimi)
- Tema değişkenleri `:root` (default = stüdyo: TURUNCU #ff8c3c/#f97316 + MOR #a855f7 — kullanıcı kuralı) ve `html[data-theme="necropunk"|"timberheim"]` bloklarında.
- Oyun kartındaki `data-set-theme` attribute'u: kartın üstüne gelince `<html data-theme=...>` değişir → TÜM sayfa (zemin, başlık, çerçeveler, fontlar) o oyunun temasına döner ve başka karta gelene dek kalır; sayfa yenilenince default'a döner. Steel Heaven kartı `data-set-theme="default"` (kendi teması yok, stüdyo kimliği — kullanıcı kararı 2026-07-23).
- Oyun kartlarının KENDİ görünümü sayfa temasından bağımsız sabittir (`.g-sh`, `.g-np`, `.g-th` sınıfları).
- **Tema efekt katmanları** (body sonunda, `pointer-events:none`, tema aktifken görünür): `#fx-scan` = Necropunk scanline; Necropunk'ta ayrıca h1 glitch (data-text + ::before/::after clip) ve buton hover'da glitch jitter + RGB split; `#fx-snow` = Timberheim yağan kar; `#fx-rune` = sağ alt köşede rünik taş (inline SVG — rün KARAKTERLERİ değil, mobilde tofu çıkmasın diye çizim; dar ekranda gizli). `prefers-reduced-motion` durumunda animasyonlar kapalı.
- Tema kaynağı: `D:\htmlprojects\stream-console\public\assets\themes.css`. NECROPUNK = neon kırmızı #ff2a4d + elektrik mavisi #00d9ff + Oxanium; TIMBERHEIM = buz mavisi #7cc7ff + köz turuncusu #ff9a3c + Metamorphous. Rün süsleri web'de KULLANILMAZ (mobilde tofu çıkarır).

## Güncelleme akışı
1. `index.html` düzenle → commit → push. Bitti.
2. Link listesinin doğruluk kaynağı: `D:\UnrealProjects\marketing\README.md` → "Sabit linkler" tablosu. Yeni link oraya da işlenir.
3. **Bekleyen işler ("Games" sütunu):**
   - STEEL HEAVEN çıkınca: alt yazı "Wishlist on Steam" → "Play now" + `OUT NOW` rozeti eklenebilir (`.badge` CSS'i hazır duruyor; SOON rozeti kullanıcı isteğiyle kaldırıldı — wishlist zaten açık).
   - Necropunk Steam sayfası açılınca: `div.game.g-np` → `<a>` (href + `data-count` + wishlist alt yazısı + SOON rozeti); `g-np` sınıfı ve `data-set-theme` kalır, `a.g-np:hover` stili hazır.
   - Timberheim linki çıkınca aynı şekilde: `div.game.g-th` → `<a>`.
   - **Custom domain (2026-07-23):** goldenstonegames.com (GoDaddy, kullanıcının; yenileme Ağu 2028). Repo'da `CNAME` dosyası var; og:url'ler yeni domain'de. DNS: 4× A kaydı (185.199.108/109/110/111.153) + `www` CNAME → byggoldenstone.github.io. Canlı doğrulanınca: GitHub Pages'te "Enforce HTTPS" aç + bio'lardaki linkler `goldenstonegames.com/?ref=...` yapılacak (eski github.io adresi otomatik yönlendirir, acele yok) + marketing README "Sabit linkler" güncellenecek.

## Tıklama sayacı
- Her dış linkte `data-count="/click-..."` attribute'u var; tıklamalar GoatCounter'a event olarak gider (panel: goldenstonegames.goatcounter.com). Yeni link eklerken `data-count` da ekle.

## Kurallar
- Sayfada oyun sloganı/rozeti YOK — stüdyo odaklı sade görünüm (kullanıcı kararı, 2026-07-15).
- İletişim: goldenstonegames@gmail.com (footer'da, kullanıcı onayıyla kamuya açık).
