# Link Hub — goldenstonegames.com

Goldenstone Games'in "tüm linkler tek sayfada" sitesi. Bio'lardaki tek link alanlarına bu URL konur.

## Yapı
- `index.html` (self-contained, harici bağımlılık yok) + `avatar.png` (480px; orijinal `D:\UnrealProjects\marketing\brand\pp-original.png`) + `fonts\` (başlık: Oxanium/Necropunk, Metamorphous/Timberheim; gövde: Rajdhani/Necropunk, Alegreya Sans/Timberheim — tema aktifken TÜM yazılar `--body-font` ile o oyunun fontuna geçer; kaynak: `D:\htmlprojects\stream-console\public\assets\fonts\`) + `icons\` (marka logoları, simple-icons SVG, fill=marka rengi gömülü; koyu zeminde X ve TikTok beyaz).
- **Public repo:** `BYGGOLDENSTONE/BYGGOLDENSTONE.github.io` — GitHub Pages, master branch kökü. Push sonrası ~1-2 dk'da canlıya geçer; kullanıcı test ederken ESKİ SÜRÜMÜ görebilir → önce deploy'u bekle, sonra **Ctrl+Shift+R** (art arda push'larda yaşandı, 2026-07-23).
- **Custom domain:** goldenstonegames.com (GoDaddy, kullanıcının; yenileme Ağu 2028; bağlandı 2026-07-23). `CNAME` dosyası repo'da; DNS = 4× A (185.199.108/109/110/111.153) + `www` CNAME → byggoldenstone.github.io; HTTPS enforced AÇIK. Eski byggoldenstone.github.io 301 ile yönlendirir (query korunur), `/t` kısa adresi de çalışır.
- Görsel doğrulama yöntemi: Chrome headless ile `--screenshot` + `--virtual-time-budget` (statik tema testi için `<html data-theme=...>` sabitlenmiş geçici kopya kullan; runtime opacity/renk geçişleri headless'ta yarım görünür, yanıltmasın).
- Favicon = `favicon.png` — avatar'ın dairesel kırpılmış, köşeleri şeffaf hali (avatar.png kare olduğu için sekmede beyaz köşe çıkarıyordu; System.Drawing ile üretildi). Avatar değişirse favicon da yeniden üretilir.
- Tüm dış linkler `target="_blank" rel="noopener"` (kullanıcı isteği).

## Düzen (2026-07-23 redesign)
- **Masaüstü (>920px): 3 sütun** — Socials | Live Development (Turkish) | Games. Amaç: 1080p'de kaydırmasız tek ekran. Dar ekranda tek sütuna düşer.
- Sosyal linkler ikonlu satır; **oyun kartları İKONSUZ** — sadece oyun adı kendi tema fontuyla, tipografi odaklı (kullanıcı kararı: emoji ikon YASAK).

## Sayfa temaları (hover ile tam sayfa tema değişimi)
- Tema değişkenleri `:root` (default = stüdyo: TURUNCU #ff8c3c/#f97316 + MOR #a855f7 — kullanıcı kuralı) ve `html[data-theme="necropunk"|"timberheim"]` bloklarında.
- Oyun kartındaki `data-set-theme` attribute'u: kartın üstüne gelince `<html data-theme=...>` değişir → TÜM sayfa (zemin, başlık, çerçeveler, fontlar) o oyunun temasına döner ve başka karta gelene dek kalır; sayfa yenilenince default'a döner. Steel Heaven kartı `data-set-theme="default"` (kendi teması yok, stüdyo kimliği — kullanıcı kararı 2026-07-23).
- Oyun kartlarının KENDİ görünümü sayfa temasından bağımsız sabittir (`.g-sh`, `.g-np`, `.g-th` sınıfları).
- **Tema efekt katmanları** (body sonunda, `pointer-events:none`, tema aktifken görünür):
  - Necropunk: `#fx-scan` scanline; `#fx-beacon` dönen kızıl fener (conic huzme, 9 sn'de bir kullanıcıya dönüp kızıl parlama); `.page`'de aralıklı sayfa geneli glitch patlamaları (7 sn döngü); h1 glitch (data-text + clip); buton/oyun hover'da TİTREME YOK (kullanıcı isteği) — hologram: holoFlicker + cyan scanline zemin + yazı dilimi kayması (label/gname'deki `data-text` kopyaları sliceGlitch A/B ile kayar). Yeni link eklerken label'a `data-text` eklemeyi unutma.
  - Timberheim: `#fx-snow` iki katmanlı kar (17s + 27s farklı periyot → tekrar hissi yok); `#fx-fire` alt ortada titreşen kamp ateşi ışığı (5.2s + 2.3s çift katman); `#fx-rune` sağ altta rünik taş (inline SVG çizim, rün karakteri değil — mobil tofu; dar ekranda gizli).
  - `prefers-reduced-motion`: animasyonlar kapalı, fener tamamen gizli.
- Tema kaynağı: `D:\htmlprojects\stream-console\public\assets\themes.css`. NECROPUNK = neon kırmızı #ff2a4d + elektrik mavisi #00d9ff + Oxanium; TIMBERHEIM = buz mavisi #7cc7ff + köz turuncusu #ff9a3c + Metamorphous. Rün süsleri web'de KULLANILMAZ (mobilde tofu çıkarır).

## Güncelleme akışı
1. `index.html` düzenle → commit → push. Bitti.
2. Link listesinin doğruluk kaynağı: `D:\UnrealProjects\marketing\README.md` → "Sabit linkler" tablosu. Yeni link oraya da işlenir.
3. **Bekleyen işler ("Games" sütunu):**
   - STEEL HEAVEN çıkınca: alt yazı "Wishlist on Steam" → "Play now" + `OUT NOW` rozeti eklenebilir (`.badge` CSS'i hazır duruyor; SOON rozeti kullanıcı isteğiyle kaldırıldı — wishlist zaten açık).
   - Necropunk Steam sayfası açılınca: `div.game.g-np` → `<a>` (href + `data-count` + wishlist alt yazısı + SOON rozeti); `g-np` sınıfı ve `data-set-theme` kalır, `a.g-np:hover` stili hazır.
   - Timberheim linki çıkınca aynı şekilde: `div.game.g-th` → `<a>`.
   - Bio'lardaki linkler zamanla `goldenstonegames.com/?ref=...` yapılacak (eski github.io adresi 301 yönlendirir, acele yok; `/kanal-kontrol` ile toplu yapılabilir).
   - **SONRAKİ SEANS:** boyut farkı / size sorunu çözülecek — 2560×1440 gibi büyük monitörlerde sayfa küçük kalıyor, farklı çözünürlüklere göre ölçekleme çalışması yapılacak (kullanıcı talebi, 2026-07-23).

## Tıklama sayacı
- Her dış linkte `data-count="/click-..."` attribute'u var; tıklamalar GoatCounter'a event olarak gider (panel: goldenstonegames.goatcounter.com). Yeni link eklerken `data-count` da ekle.

## Kurallar
- Sayfada oyun sloganı/rozeti YOK — stüdyo odaklı sade görünüm (kullanıcı kararı, 2026-07-15).
- İletişim: goldenstonegames@gmail.com (footer'da, kullanıcı onayıyla kamuya açık).
