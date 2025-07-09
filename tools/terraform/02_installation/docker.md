# 📘 Terraform 1.12.2’yi Docker Üzerinde Çalıştırma Rehberi

**Sürüm Tarihi:** 2025-07-09
**Amaç:** Terraform'u Docker container içinde kullanarak sisteminize kurulum yapmadan `.tf` dosyalarınızı çalıştırmak.

---

## 🧱 1. Gerekli Ön Koşullar

* Docker 20.10+ yüklü olmalı
* Komut satırında `docker` erişilebilir olmalı
* `.tf` dosyaları olan bir proje dizinine sahip olmalısınız

---

## 🐳 2. Terraform Docker Image’ını Çekme

```bash
docker pull hashicorp/terraform:1.12.2
```

Alternatif:

```bash
docker pull hashicorp/terraform:latest
```

---

## 🔧 3. Docker ile Terraform Komutları Çalıştırma

### Proje dizinine geç:

```bash
cd ~/projects/my-terraform
```

### Terraform init:

```bash
docker run --rm -v $(pwd):/workspace -w /workspace \
hashicorp/terraform:1.12.2 init
```

### Terraform plan:

```bash
docker run --rm -v $(pwd):/workspace -w /workspace \
hashicorp/terraform:1.12.2 plan
```

### Terraform apply:

```bash
docker run --rm -v $(pwd):/workspace -w /workspace \
hashicorp/terraform:1.12.2 apply -auto-approve
```

---

## ⚠️ 4. Dikkat Edilmesi Gereken Kritik Noktalar

| Konu                 | Açıklama                                                                  |
| -------------------- | ------------------------------------------------------------------------- |
| **State Dosyası**    | `terraform.tfstate` konteynerde kalırsa kaybolur, **volume** kullanılmalı |
| **Plugin Cache**     | `.terraform/` klasörü her seferinde yeniden oluşur, mount etmek iyi olur  |
| **Versiyon Uyumu**   | Provider dosyaları Terraform sürümüyle uyumlu olmalı                      |
| **Geçici Konteyner** | `--rm` kullanmak sistemde çöp bırakmaz, tavsiye edilir                    |

---

## 🔐 5. Güvenlik Yapılandırmaları

* **.env ile gizli veriler:**
  Örnek `.env`:

  ```ini
  HCLOUD_TOKEN=your-secret-token
  ```

  Kullanımı:

  ```bash
  docker run --rm --env-file .env \
    -v $(pwd):/workspace -w /workspace \
    hashicorp/terraform:1.12.2 plan
  ```

* `.env` dosyasını mutlaka `.gitignore` içine al:

  ```
  echo ".env" >> .gitignore
  ```

* **Root dışı kullanıcı kullanımı** (İsteğe bağlı):

  ```dockerfile
  FROM hashicorp/terraform:1.12.2
  USER nobody
  ```

---

## 🛠 6. Troubleshooting Tablosu

| Hata / Durum                     | Olası Sebep & Çözüm                                            |
| -------------------------------- | -------------------------------------------------------------- |
| `No credential providers found`  | Ortam değişkeni eksik. `.env` dosyası veya `-e` ile aktar      |
| `Plugin re-downloads every time` | `.terraform/` klasörünü volume ile mount et                    |
| `Permission denied` hatası       | Host dizin izinlerini kontrol et (`chmod 755 .`)               |
| `State file lock` problemi       | Paralel işlem varsa bekle, ya da `-lock=false` ile override et |

---

## 💡 7. İpuçları (Opsiyonel)

### Alias ile kullanım kolaylığı:

```bash
alias tf='docker run --rm -v $(pwd):/workspace -w /workspace hashicorp/terraform:1.12.2'
```

Artık:

```bash
tf init
tf plan
tf apply
```

### Makefile ile otomasyon (isteğe bağlı)

```makefile
TERRAFORM_IMAGE=hashicorp/terraform:1.12.2

init:
	docker run --rm -v $(PWD):/workspace -w /workspace $(TERRAFORM_IMAGE) init

plan:
	docker run --rm -v $(PWD):/workspace -w /workspace $(TERRAFORM_IMAGE) plan

apply:
	docker run --rm -v $(PWD):/workspace -w /workspace $(TERRAFORM_IMAGE) apply -auto-approve
```

---

## 📦 Özet Akış

```bash
docker pull hashicorp/terraform:1.12.2
cd /path/to/your/project
docker run --rm -v $(pwd):/workspace -w /workspace hashicorp/terraform:1.12.2 init
docker run --rm -v $(pwd):/workspace -w /workspace hashicorp/terraform:1.12.2 plan
docker run --rm -v $(pwd):/workspace -w /workspace hashicorp/terraform:1.12.2 apply -auto-approve
```

---

Bu yapı sayesinde:

* Hiçbir şey sistemine kurmadan,
* Terraform versiyonlarını dert etmeden,
* Güvenli ve temiz bir kullanım elde edersin.
