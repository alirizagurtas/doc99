Süper! Şimdi de Terraform'un **APT (Ubuntu) üzerinden manuel kurulum** adımlarını içeren, sade ve profesyonel bir dokümantasyon hazırlayalım. Bu, az önce yaptığımız **Docker versiyonunun kardeşi** olarak düşünülebilir.

---

# 📘 Terraform 1.x APT Üzerinden Ubuntu Kurulum Rehberi

**Sürüm Tarihi:** 2025-07-09
**Amaç:** Terraform’un en güncel sürümünü Ubuntu sistemine `apt` ile kurmak.
**Platform:** Ubuntu 20.04, 22.04, 24.04 (desteklenen sürümler)

---

## 🧱 1. Ön Gereksinimler

* Ubuntu (desteklenen sürümler)
* `sudo` erişimi olan kullanıcı
* İnternet bağlantısı

---

## 📦 2. Kurulum Adımları (Resmi Siteye Göre)

### 2.1 GPG Anahtarını Ekleyin

```bash
wget -O - https://apt.releases.hashicorp.com/gpg | \
  sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
```

### 2.2 Kaynağı Listeye Ekleyin

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com \
$(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" \
| sudo tee /etc/apt/sources.list.d/hashicorp.list
```

### 2.3 Terraform'u Kurun

```bash
sudo apt update && sudo apt install terraform
```

---

## 🔍 3. Kurulumun Doğrulanması

```bash
terraform version
```

Çıktı örneği:

```
Terraform v1.12.2
```

---

## ⚠️ 4. Dikkat Edilmesi Gereken Kritik Noktalar

| Konu                    | Açıklama                                                                 |
| ----------------------- | ------------------------------------------------------------------------ |
| **APT Kaynakları**      | HashiCorp deposu eklenmeden `apt install terraform` eski sürüm kurabilir |
| **Sürüm Sabitleme**     | Belirli sürüme kilitlemek için: `sudo apt install terraform=1.12.2-1`    |
| **Güncelleme Yönetimi** | `apt upgrade` ile yeni sürüme geçiş olur, proje uyumluluğuna dikkat      |

---

## 🔐 5. Güvenlik ve Sistem İpuçları

* Kurulan binary şurada olur: `/usr/bin/terraform`
* Sudo olmadan çalıştırmak için:

  ```bash
  chmod +x ~/.local/bin && export PATH="$HOME/.local/bin:$PATH"
  ```
* Eğer Vault, Consul vb. HashiCorp araçları da kurulacaksa aynı `apt` kaynakları kullanılabilir.

---

## 🛠 6. Troubleshooting Tablosu

| Sorun / Durum                        | Olası Sebep & Çözüm                                             |
| ------------------------------------ | --------------------------------------------------------------- |
| `terraform: command not found`       | Kurulum başarısız veya `PATH` içinde değil                      |
| `Unable to locate package terraform` | Kaynak eklenmemiş ya da `apt update` yapılmamış                 |
| GPG hatası                           | `--dearmor` satırı eksik veya GPG bağlantısı başarısız          |
| Sürüm uyuşmazlığı                    | `terraform -version` ile kontrol edip gerekiyorsa downgrade yap |

---

## 💡 7. Ekstra Bilgiler

### Terraform'u Belirli Bir Sürüme Kilitleme

```bash
sudo apt install terraform=1.12.2-1
```

> Tüm mevcut sürümleri listelemek için:

```bash
apt list -a terraform
```

---

## 📦 Özet Akış

```bash
wget -O - https://apt.releases.hashicorp.com/gpg | \
  sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com \
$(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" \
| sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update && sudo apt install terraform
```

---

## ✅ Sonuç

Bu yöntem:

* Kurulumu doğrudan sistemine yapar
* IDE (VS Code vb.) ile yerel çalışma için uygundur
* Güncellemeler sistem paket yöneticisiyle yönetilir (`apt upgrade`)

---

İstersen:

* Aynı yapıda bir **Manuel Binary Kurulum Rehberi** (ZIP dosyası indirip `$PATH`’e atma)
* Terraform versiyon yönetimi için `tfenv` kurulumunu
* Ya da HashiCorp’un diğer araçları için benzer dökümanları da hazırlayabilirim.

Hazırsan bir sonraki adımı belirleyelim:
`tfenv`, `terraform-ls` ya da VS Code eklentileri gibi konulara geçebiliriz.
