# Yorgun Demokrat — Discord Botu

Yorgun ama nazik bir Discord botu: slash komutları ve mesaj tetikleyicileri.

## Kurulum

1. [Discord Developer Portal](https://discord.com/developers/applications) üzerinden yeni bir **Application** oluştur.
2. **Bot** sekmesinden botu ekle, **TOKEN**'ı kopyala.
3. **Privileged Gateway Intents** altında **Message Content Intent**'i aç (mesajda "yorgun demokrat" algılaması için).
4. **OAuth2 → URL Generator**: `bot` + `applications.commands` scope'larını seç; bot izinlerinde en az **Send Messages**, **Embed Links**, **Read Message History**, **Connect**, **Speak** işaretle. URL ile sunucuna ekle.
5. Projede:

```bash
npm install
npm approve-scripts ffmpeg-static
cp .env.example .env
# .env içine DISCORD_TOKEN ve DISCORD_CLIENT_ID yaz
npm run deploy-commands
npm start
```

Müzik **yt-dlp** (`youtube-dl-exec`) ve **ffmpeg-static** kullanır; ilk `npm install` sırasında yt-dlp ikilisi indirilebilir (birkaç dakika). Sorun olursa **Node 20 LTS** dene.

Geliştirme sırasında `npm run dev` dosya değişince botu yeniden başlatır.

### Komutları sadece test sunucusunda kaydetmek

`.env` dosyasına `DISCORD_GUILD_ID=sunucu_id` ekle, sonra `npm run deploy-commands` çalıştır. Global yayılım beklemeden komutlar görünür.

## Komutlar

| Komut | Açıklama |
|--------|----------|
| `/y play sarki:…` | YouTube/Spotify parça, **playlist**, albüm veya şarkı adı (playlist max 50 parça) |
| `/y radio` | Playlist (TR/Global) + [Karnaval.com](https://karnaval.com/) canlı radyolar |
| `/y stop` | Durdur, ses kanalından çık |
| `/ping` | Gecikme |
| `/soz` | Rastgele söz |
| `/yorgunluk` | Yorgunluk yüzdesi |
| `/yardim` | Yardım |

## Yapı

```
src/
  commands/     slash komutları
  data/         sözler ve metinler
  index.js      bot girişi
  deploy-commands.js
```

Yeni komut: `src/commands/` altına `data` + `execute` export eden bir dosya ekle, `npm run deploy-commands` ile Discord'a kaydet.
