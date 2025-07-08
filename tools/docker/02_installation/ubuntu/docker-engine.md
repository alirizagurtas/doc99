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

### ✅ **DOCKER ENGINE KURULUMU** (Resmi Dökümana Göre)
*(Kaynak: [Engine Install Docs](https://docs.docker.com/engine/install/ubuntu/))*

#### 📋 ÖNKOŞULLAR
```bash
# 1. Eski sürümleri temizle:
sudo apt remove docker.io docker-doc docker-compose podman-docker containerd runc

# 2. Bağımlılıkları kur:
sudo apt update
sudo apt install ca-certificates curl
```

#### 🔧 KURULUM ADIMLARI
```bash
# 1. Resmi GPG anahtarını ekle:
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# 2. Repository ekle:
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# 3. Paket listesini güncelle:
sudo apt update

# 4. Docker Engine'i kur (son sürüm):
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# 5. Test çalıştır:
sudo docker run hello-world
```

#### ⚙️ Temel Yapılandırma
```bash
# Kullanıcıyı docker grubuna ekle (sudo'suz kullanım için):
sudo usermod -aG docker $USER
newgrp docker

# Servisi etkinleştir:
sudo systemctl enable docker
sudo systemctl start docker
```

---

### 🆚 Karşılaştırmalı Kurulum Tablosu
| Adım | Docker Desktop | Docker Engine |
|------|---------------|--------------|
| **Depo Ekleme** | ✅ Aynı | ✅ Aynı |
| **Paket İsmi** | `docker-desktop` | `docker-ce` |
| **GUI Desteği** | ✅ Var | ❌ Yok |
| **Kubernetes** | ✅ Entegre | ❌ Manuel kurulum |
| **CLI Araçları** | `docker`, `kubectl` | Sadece `docker` |
| **Lisans** | Ücretli (kurumsal) | Tamamen ücretsiz |
| **Tipik Kullanım** | Lokal geliştirme | Sunucu/CI ortamları |

---

### ❓ "Hangisini Kullanmalıyım?" Rehberi
1. **Ubuntu Sunucusu** üzerinde çalışıyorsanız → **Docker Engine**
2. **Kişisel Ubuntu Masaüstü** ve konteyner geliştirme yapıyorsanız → **Docker Desktop**
3. **Kubernetes test ortamı** istiyorsanız → **Docker Desktop** (entegre Kubernetes)
4. **Ücretsiz ve hafif** çözüm istiyorsanız → **Docker Engine**

Her iki kurulum da resmi dökümanlarda geçerli, sadece farklı kullanım senaryoları için tasarlanmıştır.
