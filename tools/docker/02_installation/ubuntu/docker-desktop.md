### 🔍 Temel Fark: Docker Desktop vs Docker Engine
| Özellik | **Docker Desktop** | **Docker Engine** |
|---------|-------------------|------------------|
| **İçerik** | GUI + Engine + Kubernetes + Container Management | Sadece CLI tabanlı Docker Engine |
| **Kullanım** | Geliştiriciler için (GUI desteği) | Sunucular/CI/CD için (headless) |
| **Lisans** | [Ücretli kurumsal sürüm](https://www.docker.com/pricing/) | Tamamen ücretsiz |
| **Paket** | `.deb` (tümleşik) | `docker-ce`, `containerd.io` (ayrı paketler) |

---

### 🖥️ **HANGİSİNİ KURMALI?**
- **Masaüstünde çalışıyorsanız** (GUI istiyorsanız) → **Docker Desktop**
- **Sunucu/CLI ortamında çalışıyorsanız** → **Docker Engine**

---

### **DOCKER DESKTOP UBUNTU KURULUM DOKÜMANI**
**Kaynak:** [Docker Official Docs](https://docs.docker.com/desktop/setup/install/linux/ubuntu/)
**Doğrulama Tarihi:** 9 Temmuz 2025
**Kapsam:** Ubuntu 22.04/24.04 (GNOME/KDE)

---

### ✅ **KONTROL LİSTESİ: ÖNKOŞULLAR**
1. [ ] **Sistem mimarisi**: `x86-64` (Kontrol: `arch` komutu)
2. [ ] **Ubuntu Sürümü**:
    - Ubuntu 22.04 LTS (Jammy)
    - Ubuntu 24.04 LTS
    - En son non-LTS sürüm
    *(Kontrol: `lsb_release -a`)*
3. [ ] **Masaüstü Ortamı**:
    - GNOME/KDE dışı kullanıyorsanız:
      ```bash
      sudo apt install gnome-terminal -y
      ```

---

### 🔧 **KURULUM ADIMLARI (SIRALI)**

#### **1. AŞAMA: RESMİ DOCKER REPOSİTORY KURULUMU**
*(Zorunlu temel altyapı)*
```bash
# 1. Güncelleme ve bağımlılıklar
sudo apt-get update
sudo apt-get install ca-certificates curl -y

# 2. GPG anahtar ekleme
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# 3. Repository ekleme
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

#### **2. AŞAMA: DOCKER DESKTOP PAKET KURULUMU**
*(Ana uygulama yüklemesi)*
```bash
# 1. Son sürüm DEB paketini indir
wget https://desktop.docker.com/linux/main/amd64/docker-desktop-amd64.deb

# 2. Paketi yükle (HATA UYARISINI GÖRMEZDEN GELİN)
sudo apt-get install ./docker-desktop-amd64.deb -y
```
> **NOT:** `Permission denied` uyarısı normaldir, kurulum başarıyla tamamlanır.

#### **3. AŞAMA: KURULUM SONRASI YAPILANDIRMA**
*(Otomatik tamamlanır)*
- [ ] Binary yetkilendirmeleri
- [ ] `/etc/hosts` güncellemesi (Kubernetes için)
- [ ] Symlink oluşturma:
  `/usr/local/bin/com.docker.cli → /usr/bin/docker`

---

### ▶️ **BAŞLATMA VE TEST**
```bash
# 1. Servisi başlat
systemctl --user start docker-desktop

# 2. Sistem açılışta otomatik başlatma
systemctl --user enable docker-desktop

# 3. Test çalıştırması
docker run --rm hello-world
```
**Beklenen Çıktı:**
`Hello from Docker!` mesajı ve sürüm bilgisi.

---

### ⚠️ **KRİTİK UYARILAR**
1. **Lisans Sınırlaması**:
   > 250+ çalışan veya $10M+ yıllık gelir → [Ücretli lisans](https://www.docker.com/pricing/) gerekir.

2. **Hata Çözümleri**:
   - `Permission denied` hatası → **Görmezden gelinebilir**
   - Başlatma hatası → `journalctl --user-unit=docker-desktop` ile log kontrol

---

### 🔄 **GÜNCELLEME PROSEDÜRÜ**
```bash
# 1. Yeni DEB paketini indir
wget https://desktop.docker.com/linux/main/amd64/docker-desktop-amd64.deb

# 2. Üzerine yükle
sudo apt-get install ./docker-desktop-amd64.deb -y
```

---

### 📝 **DOKÜMASYON REFERANSLARI**
1. [Resmi Kurulum Dokümanı](https://docs.docker.com/desktop/setup/install/linux/ubuntu/)
2. [Troubleshooting Rehberi](https://docs.docker.com/desktop/troubleshoot/overview/)
3. [Lisans Koşulları](https://www.docker.com/pricing/)

---

**Not:** Tüm komutlar root yetkisi gerektirir (`sudo`). Kurulum tamamlandığında `/opt/docker-desktop` dizinine yüklenir.
