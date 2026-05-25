# 🎮 FiveM Discord Yönetim Botu

Modern Discord v2 embed sistemi ile geliştirilmiş, FiveM sunucuları için kapsamlı yönetim ve istatistik botu.

## 📋 İçindekiler

- [Özellikler](#-özellikler)
- [Kurulum](#-kurulum)
- [Yapılandırma](#-yapılandırma)
- [Komutlar](#-komutlar)
- [Sistemler](#-sistemler)
- [Dosya Yapısı](#-dosya-yapısı)

## ✨ Özellikler

### 🎫 Ticket Sistemi
- Çoklu kategori desteği (IC, OOC, Donate, Bug)
- Ticket claim ve transfer sistemi
- Otomatik transcript oluşturma
- Detaylı ticket istatistikleri

### 📊 İstatistik Sistemi
- Personel performans takibi
- Gerçek zamanlı istatistikler
- 6 farklı kategori (Özet, Ticket, IC, Kayıt/WL, Ekip, Destek)
- Periyodik raporlama (Günlük/Haftalık/Aylık)
- Liderlik tablosu ve grafikler

### 👥 Kullanıcı Yönetimi
- Whitelist sistemi (onay paneli ile)
- Kayıtsız atama
- IC isim onay/red sistemi
- Kullanıcı geçmişi ve sicil takibi
- Ban/Unban yönetimi

### 🛡️ Moderasyon
- Ceza sistemi (çarpan ve süre desteği)
- Sicil kayıtları
- Toplu rol yönetimi
- Toplu susturma
- Destek kayıt sistemi

### 🎭 Rol Yönetimi
- Rol verme/alma
- Toplu rol işlemleri
- Rol geçmişi takibi
- Context menu entegrasyonu

### 🏢 Ekip Sistemi
- Dinamik ekip kanalları
- Ekip üye yönetimi
- Ekip kapatma/açma takibi

### 📢 Sunucu Duyuruları
- Aktif/Bakım/Restart duyuruları
- v2 embed tasarımı
- Özelleştirilebilir görseller

## 🚀 Kurulum

### Gereksinimler
- Node.js v18 veya üzeri
- MongoDB
- Discord Bot Token

### Adımlar

1. **Projeyi klonlayın**
```bash
git clone <repo-url>
cd test_fivem_bots
```

2. **Bağımlılıkları yükleyin**
```bash
npm install
```

3. **Ortam değişkenlerini ayarlayın**
```bash
cp .env.example .env
```

`.env` dosyasını düzenleyin:
```env
DISCORD_TOKEN=your_bot_token
DISCORD_CLIENT_ID=your_client_id
DISCORD_GUILD_ID=your_guild_id
MONGODB_URI=mongodb://localhost:27017/fivem_bot
```

4. **Config dosyasını düzenleyin**
`config/config.json` dosyasını sunucunuza göre yapılandırın.

5. **Komutları deploy edin**
```bash
npm run deploy-commands
```

6. **Botu başlatın**
```bash
npm start
```

## ⚙️ Yapılandırma

### config/config.json

```json
{
  "bot": {
    "readyMessage": "✅ {botTag} hazır! {guildCount} sunucuda aktif.",
    "embedColor": "#393A41",
    "footer": "Sunucu Adı"
  },
  "ids": {
    "staffRole": "STAFF_ROLE_ID",
    "botCommandRole": "BOT_COMMAND_ROLE_ID",
    "roles": {
      "whitelist": "WHITELIST_ROLE_ID",
      "kayitsiz": "KAYITSIZ_ROLE_ID",
      "karakterOnay": "KARAKTER_ONAY_ROLE_ID",
      "banhammer": "BANHAMMER_ROLE_ID",
      "ustYonetim": "UST_YONETIM_ROLE_ID",
      "ekipSorumlusu": "EKIP_SORUMLUSU_ROLE_ID"
    },
    "channels": {
      "ticketLog": "TICKET_LOG_CHANNEL_ID",
      "whitelistLog": "WHITELIST_LOG_CHANNEL_ID",
      "icIsimLog": "IC_ISIM_LOG_CHANNEL_ID",
      "roleLog": "ROLE_LOG_CHANNEL_ID",
      "banLog": "BAN_LOG_CHANNEL_ID",
      "cezalar": "CEZALAR_CHANNEL_ID",
      "cezaLog": "CEZA_LOG_CHANNEL_ID",
      "destekLog": "DESTEK_LOG_CHANNEL_ID"
    },
    "categories": {
      "parent": "PARENT_CATEGORY_ID",
      "ekip": "EKIP_CATEGORY_ID",
      "ic": "IC_CATEGORY_ID",
      "ooc": "OOC_CATEGORY_ID",
      "donate": "DONATE_CATEGORY_ID",
      "bug": "BUG_CATEGORY_ID"
    }
  },
  "whitelist": {
    "requireSteam": false,
    "requireHex": false,
    "limits": {
      "verPerDay": 0,
      "kayitsizPerDay": 0
    }
  },
  "fivem": {
    "serverName": "Sunucu Adı",
    "connectCommand": "connect 127.0.0.1:30120",
    "images": {
      "aktif": "IMAGE_URL",
      "bakim": "IMAGE_URL",
      "restart": "IMAGE_URL"
    }
  }
}
```

## 📝 Komutlar

### Yönetim Komutları

| Komut | Açıklama | Yetki |
|-------|----------|-------|
| `/ticket-panel` | Ticket panelini oluşturur | Administrator |
| `/aktif` | Sunucu aktif duyurusu | Üst Yönetim |
| `/bakim` | Sunucu bakım duyurusu | Üst Yönetim |
| `/restart` | Sunucu restart duyurusu | Üst Yönetim |

### Kullanıcı Yönetimi

| Komut | Açıklama | Yetki |
|-------|----------|-------|
| `/whitelist ver` | Whitelist verir (onay paneli ile) | Staff |
| `/kayitsiz` | Kullanıcıyı kayıtsıza atar | Bot Command |
| `/kullanici-bilgi` | Kullanıcı bilgilerini gösterir | Staff |
| `/ban` | Kullanıcıyı banlar | Banhammer |
| `/unban` | Ban kaldırır | Banhammer |
| `/ban-bilgi` | Ban bilgilerini gösterir | Staff |

### İstatistik Komutları

| Komut | Açıklama | Yetki |
|-------|----------|-------|
| `/stat` | Personel istatistiklerini gösterir | Staff |
| `/staff-top` | Liderlik tablosunu gösterir | Üst Yönetim |
| `/top-stat` | Sunucu liderlik tablosu | Bot Command |

### Moderasyon

| Komut | Açıklama | Yetki |
|-------|----------|-------|
| `/ceza-ekle` | Kullanıcıya ceza ekler | Staff |
| `/sicil` | Kullanıcının sicil kaydını gösterir | Staff |
| `/destek` | Destek kaydı oluşturur | Staff |

### Rol Yönetimi

| Komut | Açıklama | Yetki |
|-------|----------|-------|
| `/rol ver` | Kullanıcıya rol verir | Bot Command / Manage Roles |
| `/rol al` | Kullanıcıdan rol alır | Bot Command / Manage Roles |
| `/toplu-rol ver` | Toplu rol verir | Bot Command |
| `/toplu-rol al` | Toplu rol alır | Bot Command |
| `/rollog` | Rol geçmişini gösterir | Bot Command |
| `/rolbilgi` | Rol bilgilerini gösterir | Bot Command |

### Ekip Yönetimi

| Komut | Açıklama | Yetki |
|-------|----------|-------|
| `/ekipolustur` | Yeni ekip kanalı oluşturur | Ekip Sorumlusu |

### Diğer

| Komut | Açıklama | Yetki |
|-------|----------|-------|
| `/ip` | Sunucu bağlantı bilgisi | Herkes |
| `/ysay` | Seste olmayan staffları etiketler | Bot Command |
| `/mulakat-panel-kur` | Mülakat panelini kurar | Bot Command |

### Context Menu Komutları

- **Whitelist Ekle** - Kullanıcıya sağ tıklayarak whitelist ver
- **Rol Ekle** - Kullanıcıya sağ tıklayarak rol ver
- **Rol Al** - Kullanıcıdan sağ tıklayarak rol al

## 🔧 Sistemler

### 1. Ticket Sistemi

**Özellikler:**
- 4 farklı kategori (IC, OOC, Donate, Bug)
- Ticket claim sistemi
- Ticket transfer
- Üye ekleme
- Otomatik transcript
- Detaylı istatistik takibi

**Kullanım:**
1. `/ticket-panel` ile paneli oluşturun
2. Kullanıcılar kategori seçerek ticket açar
3. Yetkili ticket'ı claim eder
4. İşlem bitince ticket kapatılır

### 2. Whitelist Sistemi

**Özellikler:**
- Onay paneli ile güvenli whitelist verme
- Kullanıcı geçmişi görüntüleme
- Son 5 giriş/çıkış kaydı
- Sicil kontrolü
- Onay/Red butonları

**Kullanım:**
1. `/whitelist ver @kullanıcı` komutu
2. Onay paneli açılır (kullanıcı bilgileri, geçmiş, sicil)
3. ✅ Onay veya ❌ Red butonuna tıkla
4. Onaylanırsa whitelist rolü verilir

### 3. Ceza Sistemi

**Özellikler:**
- Otomatik ceza numarası
- Çarpan sistemi (örn: 15x ceza)
- Süre desteği (gün bazında)
- Otomatik bitiş tarihi hesaplama
- İki log kanalı (public ve private)
- Sicil entegrasyonu

**Kullanım:**
```
/ceza-ekle @kullanıcı "Kural ihlali" 15 5
```
- 15x çarpan
- 5 gün ceza
- Bitiş tarihi otomatik hesaplanır

### 4. Destek Sistemi

**Özellikler:**
- Desteği alan yetkililer (1+)
- Destekte bulunan stafflar (1+)
- Ceza alan kişiler (opsiyonel)
- Destek açıklaması
- Otomatik istatistik güncelleme
- Log sistemi

**Kullanım:**
```
/destek 
  alan-yetkililer: @yetkili1 @yetkili2
  veren-stafflar: @staff1 @staff2
  aciklama: "Kullanıcı hesap problemi çözüldü"
  ceza-alanlar: @kullanıcı (opsiyonel)
```

### 5. İstatistik Sistemi

**Özellikler:**
- 6 farklı sekme:
  - **Genel Özet:** Tüm istatistiklerin özeti + detay butonları
  - **Ticket:** Ticket istatistikleri ve kategoriler
  - **IC İsim:** IC onay/red istatistikleri
  - **Kayıt / WL:** Whitelist ve kayıtsız istatistikleri
  - **Ekip:** Ekip açma/kapatma istatistikleri
  - **Destek:** Destek alınan/verilen istatistikleri
- Periyodik raporlama (Günlük/Haftalık/Aylık)
- Sıralama sistemi
- Performans metrikleri

**Kullanım:**
```
/stat @kullanıcı
```
- Genel Özet'te her bilgi için "Detay" butonu
- Detay butonuna tıklayarak ilgili sekmeye git
- Diğer sekmelerden "Ana Sayfaya Dön" ile özete dön

### 6. Staff Top (Liderlik Tablosu)

**Özellikler:**
- 4 kategori liderlik tablosu:
  - Kayıt Yapan (Top 5)
  - Ticket İlgilenen (Top 5)
  - IC İsim Onaylayan (Top 5)
  - Destek Alan (Top 5)
- Dinamik grafik (QuickChart API)
- Güncelleme butonu
- Son güncelleme zamanı

**Kullanım:**
```
/staff-top
```
- Liderlik tabloları ve grafik görüntülenir
- 🔄 Güncelle butonuna tıklayarak yenile

### 7. Rol Yönetimi

**Özellikler:**
- Tek ve toplu rol işlemleri
- Rol geçmişi takibi
- Context menu entegrasyonu
- Detaylı log sistemi
- Yetki kontrolü (Administrator, ManageRoles, BotCommand)

**Kullanım:**
```
/rol ver @kullanıcı @rol
/toplu-rol ver @rol @kişi1 @kişi2 @kişi3
```

### 8. Ekip Sistemi

**Özellikler:**
- Dinamik ekip kanalları
- Ekip sahibi yönetimi
- Üye ekleme/çıkarma
- Ekip kapatma
- Ban sistemi

**Kullanım:**
```
/ekipolustur "Ekip Adı" @ekip-sahibi
```

## 📁 Dosya Yapısı

```
test_fivem_bots/
├── config/
│   └── config.json              # Ana yapılandırma dosyası
├── src/
│   ├── commands/                # Slash komutları
│   │   ├── stat.js
│   │   ├── whitelist.js
│   │   ├── ceza-ekle.js
│   │   ├── destek.js
│   │   └── ...
│   ├── constants/               # Sabit değerler ve mesajlar
│   │   ├── stat.js
│   │   ├── whitelist.js
│   │   ├── ceza.js
│   │   ├── destek.js
│   │   └── ...
│   ├── database/
│   │   ├── connect.js
│   │   └── models/              # MongoDB modelleri
│   │       ├── StaffStats.js
│   │       ├── Penalty.js
│   │       ├── Support.js
│   │       ├── Ticket.js
│   │       └── ...
│   ├── events/                  # Discord event handler'ları
│   │   ├── interactionCreate.js
│   │   ├── ready.js
│   │   └── ...
│   ├── services/                # İş mantığı
│   │   ├── statPanelService.js
│   │   ├── whitelistService.js
│   │   ├── cezaService.js
│   │   ├── destekService.js
│   │   ├── staffTopService.js
│   │   └── ...
│   ├── utils/                   # Yardımcı fonksiyonlar
│   │   ├── embedBuilder.js
│   │   ├── permissions.js
│   │   ├── format.js
│   │   └── ...
│   ├── config/
│   │   └── loadConfig.js        # Config yükleyici
│   ├── index.js                 # Ana giriş noktası
│   └── deploy-commands.js       # Komut deployment
├── .env.example                 # Örnek ortam değişkenleri
├── .gitignore
├── package.json
└── README.md
```

## 🎨 Özelleştirme

### Mesajları Değiştirme

Tüm mesajlar `src/constants/` klasöründe bulunur:

```javascript
// src/constants/stat.js
module.exports = {
  panel: {
    header: '### 📊 {user} — {page}',
    // ...
  }
};
```

### Embed Renklerini Değiştirme

`config/config.json` dosyasında:

```json
{
  "bot": {
    "embedColor": "#393A41"
  }
}
```

### Görselleri Değiştirme

```json
{
  "fivem": {
    "images": {
      "aktif": "https://your-image-url.png",
      "bakim": "https://your-image-url.png",
      "restart": "https://your-image-url.png"
    }
  }
}
```

## 🔒 Güvenlik

- Tüm hassas bilgiler `.env` dosyasında saklanır
- `.env` dosyası `.gitignore`'a eklenmiştir
- Yetki kontrolleri her komutta yapılır
- MongoDB bağlantısı güvenli şekilde yapılandırılmıştır



## 📄 Lisans

Bu proje MIT lisansı altında lisanslanmıştır.


## 📞 İletişim

Sorularınız için Discord üzerinden ulaşabilirsiniz ("apozinyo").


---

**Not:** Bu bot FiveM sunucuları için özel olarak geliştirilmiştir ve Discord.js v14 ile modern v2 embed sistemi kullanmaktadır.
