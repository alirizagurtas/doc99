<!-- AI-PROMPT: CLI-DOC ===================================================
KULLANICIYA SOR (sırayla):
1. Komut/araç?      (örn. fdisk)
2. Dağıtım + sürüm? (örn. Ubuntu 24.04)

YAPAY ZEKA TALİMATLARI (özet):
- Güncel **resmî** kaynaklardan sürüm, tam parametre listesi ve pratik senaryolar çıkar
- **Tüm** parametreleri tabloya ekle; her parametre için en az bir canlı örnek ver
- Gerçek-hayat senaryoları ve komut çıktılarının özetini göster
- Riskli işlemlerde ⚠️ uyarısı, `sudo` gereksinimini vurgula
- Belge dili **tamamen Türkçe**, Markdown uyumlu
- **Platform Notları** başlığı **ÜRETME**
- **SSS** bölümünde en az 5 sık sorulan (tek satır) Q-A + “Kaynak” satırı olmalı
========================================================================= -->

{{komut}} — {{dağıtım_sürümü}}

Sürüm: `{{komut}} --version` ⇒ `{{çıktı}}`
Oluşturma Tarihi: `{{tarih}}`

---

📌 **Kısa Tanım**
{{komut}}; {{kısa_tanım}}.

---

📋 **Söz Dizimi**
```

{{komut}} {{parametre}} {{argüman}}

````

---

⚙️ **Tüm Parametreler ve Hızlı Örnekler**

| Parametre         | Açıklama           | Canlı Örnek            | Beklenen Çıktı/Kayıt |
|-------------------|--------------------|------------------------|----------------------|
| `-h, --help`      | Yardım ekranı      | `{{komut}} --help`     | Yardım metni         |
| `{{parametre_1}}` | {{açıklama_1}}     | `{{örnek_1}}`          | `{{çıktı_1}}`        |
| `{{parametre_2}}` | {{açıklama_2}}     | `{{örnek_2}}`          | `{{çıktı_2}}`        |
<!-- Man veya resmî dokümandaki tüm bayraklar burada listelenir. -->

---

💡 **Temel Kullanımlar**

```bash
# Örnek 1
{{temel_kullanım_1}}

# Örnek 2
{{temel_kullanım_2}}
````

---

🛠️ **Gelişmiş Senaryolar**

1. **{{senaryo\_başlığı\_1}}**

   ```bash
   {{senaryo_komut_1}}
   ```

   {{senaryo\_açıklama\_1}}

2. **{{senaryo\_başlığı\_2}}**

   ```bash
   {{senaryo_komut_2}}
   ```

   {{senaryo\_açıklama\_2}}

3. **{{senaryo\_başlığı\_3}}**

   ```bash
   {{senaryo_komut_3}}
   ```

   {{senaryo\_açıklama\_3}}

---

🛡️ **Güvenlik / Riskler**

| Komut              | Risk           | Güvenli Alternatif |
| ------------------ | -------------- | ------------------ |
| `{{risk_komut_1}}` | ⚠️ {{risk\_1}} | `{{alternatif_1}}` |
| `{{risk_komut_2}}` | ⚠️ {{risk\_2}} | `{{alternatif_2}}` |

---

🧑‍🏫 **Best Practices**

* {{pratik\_kural\_1}}
* {{pratik\_kural\_2}}
* {{pratik\_kural\_3}}
* {{pratik\_kural\_4}}
* {{pratik\_kural\_5}}

---

🐞 **Sorun Giderme**

| Belirti        | Olası Sebep  | Çözüm        |
| -------------- | ------------ | ------------ |
| {{belirti\_1}} | {{sebep\_1}} | {{çözüm\_1}} |
| {{belirti\_2}} | {{sebep\_2}} | {{çözüm\_2}} |

---

🔄 **Çıkış Kodları**

| Kod            | Anlam          |
| -------------- | -------------- |
| `0`            | Başarılı       |
| `1`            | Genel hata     |
| `{{özel_kod}}` | {{özel\_hata}} |

---

🔗 **İlgili Komutlar**
`{{ilgili_komut_1}}`, `{{ilgili_komut_2}}`, `{{ilgili_komut_3}}`

---

❅ **SSS**

**S:** {{soru\_1}}
**C:** {{cevap\_1}}

**S:** {{soru\_2}}
**C:** {{cevap\_2}}

**S:** {{soru\_3}}
**C:** {{cevap\_3}}

**S:** {{soru\_4}}
**C:** {{cevap\_4}}

**S:** {{soru\_5}}
**C:** {{cevap\_5}}
