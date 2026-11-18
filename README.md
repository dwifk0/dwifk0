<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/dwifk0/dwifk0/main/varlik/banner-koyu.svg">
  <img alt="Ahmet Efe Nezli — Gömülü Sistemler, Robotik, Kontrol" src="https://raw.githubusercontent.com/dwifk0/dwifk0/main/varlik/banner-acik.svg">
</picture>

Manisa Celâl Bayar Üniversitesi Elektrik-Elektronik Mühendisliği lisans
öğrencisiyim. Çalışmalarım gömülü sistemlerin **kart seviyesinde** yoğunlaşıyor:
gerçek zamanlı kontrol, emniyet mimarisi ve sensör entegrasyonu.

İki TEKNOFEST takımında gömülü sistemler ve donanım sorumluluğunu yürütüyorum —
bir otonom kara aracı ve bir hava savunma taret sistemi. Öncesinde dört yıl FLL
ve FRC.

> **English:** Electrical-electronics engineering student at Manisa Celal Bayar
> University, working on board-level embedded systems — real-time control, safety
> architecture and sensor integration. Embedded lead on a TEKNOFEST 2026 finalist
> autonomous ground vehicle and on an air-defence turret. Every repository below has
> an English README.

---

## Neler yaptım

### 🚜 LYDİA — Otonom Kara Aracı · TEKNOFEST 2026 **finalist**
**MCBÜ MAGNESİA** · Gömülü Sistemler ve Donanım Entegrasyon Sorumlusu
→ **[`IKA-MAGNESIA-LYDIA`](https://github.com/dwifk0/IKA-MAGNESIA-LYDIA)**

48 V'luk aracın **bütün sürüş ve sensör yazılımını tek bir STM32F767ZI'de**
topladım: kumanda, gaz, fren, direksiyon, geri vites, güç kesme. Jetson Orin
Nano ile arasındaki seri köprüyü, ROS 2 arayüzünü, manuel/otonom kip hakemini
ve donanım acil stop zincirini kurdum. Enkoder ve IMU verisinden odometri
üreterek otonom kipte daha kararlı bir ilerleme sağladım.

*Araç, Eylül 2026'da Mardin'de düzenlenen finale **finalist olarak** katıldı.*

### 🛡️ MİĞFER — Hava Savunma Taret Sistemi · TEKNOFEST Çelikkubbe
**MCBÜ SAVSİSTEK** · Gömülü Sistemler ve Yapay Görü Sorumlusu
→ **[`hss26-gomulu-public`](https://github.com/dwifk0/hss26-gomulu-public)**

ESP32-S3 ana firmware'i: 50 kHz kesme içinde **DDS adım üreteciyle** pan-tilt
hareketi, yasak alan kilidi, kopuk kabloyu "basılı" okuyan mandallı acil stop
zinciri, güç tüketimi izleme. Raspberry Pi 5 ve Hailo-8L NPU üzerinde çalışan
gerçek zamanlı tespit hattını kurdum. PyQt6 yer kontrol arayüzüyle taret
arasındaki TCP köprüsünü, görüntüden hedef takibini ve atış karar mantığını
geliştirdim. Sistem, açılışta kendiliğinden ayağa kalkan üç systemd servisine
bağlı olarak çalışıyor.

### 🔭 Diğer açık depolar
- **[`orbbec-gemini335l-ros2`](https://github.com/dwifk0/orbbec-gemini335l-ros2)** —
  Orbbec Gemini 335L derinlik kamerasını WSL2, Jetson ve Raspberry Pi üzerinde ROS 2
  ile çalıştırma kılavuzu: ölçümle doğrulanmış 12 gerçek sorun, nedeni ve çözümü.
- **[`orientation-cube`](https://github.com/dwifk0/orientation-cube)** — ESP32 + BMI160
  ile gerçek zamanlı yönelim ölçümü, tamamlayıcı filtre, mikrodenetleyicide 3B küp
  çizimi ve masaüstünde koşan birim testler.

### 🤖 BALROB — FIRST Robotics (FRC #8555) ve FLL · lise, 2020–2024
**Elektronik-Gömülü Sistemler Sorumlusu**

FRC 2022 (RAPID REACT, İzmir Regional) robot kodunu Java/WPILib ile yazdım: NavX
gyro, SparkMax asansör, top alma mekanizması ve otonom kip. FLL'de EV3 robotlarını
gyro PID ile programladım. Takımın elektronik altyapısını ve RoboRIO entegrasyonunu
yönettim.

---

## Çalıştığım katmanlar

Yalnız açık depolarda kanıtı olanlar:

```
firmware    STM32F767 (C++, PlatformIO) · ESP32-S3 · ESP32 · kesme içinde gerçek zamanlı iş
            platformdan bağımsız karar çekirdeği + masaüstünde birim testler
emniyet     iki kanallı donanım acil stop · kopuk kabloyu "basılı" okuyan mandal · güç kesme
veriyolu    UART (8 baytlık özel protokol) · I²C · SPI · PWM · iBUS · USB CDC
donanım     step sürücü (TB6600 / DM860) · şönt akım ölçümü (INA226) · BMS telemetrisi (BLE)
sistem      Jetson Orin Nano · Raspberry Pi 5 · Ubuntu · systemd · udev · Docker · ROS 2 arayüzü
yapay görü  YOLOv8 → Hailo-8L (Dataflow Compiler) · OpenCV
araç        Python tezgah ve saha panoları · PyQt6 · Git
öğreniyorum CAN · KiCad ile kart tasarımı · güvenli bootloader · FPGA (Verilog)
```

## Mühendislik yaklaşımım

**Doğrulanabilirlik.** Tasarım kararlarını ölçüme dayandırırım; paylaştığım her
değer ya ölçülmüştür ya da nasıl ölçüldüğü belgesinde yer alır. Varsayımla
ilerleyen bir tasarımın bedeli sahada ödenir.

**Emniyet, sonradan eklenen bir katman değildir.** Kritik kesme yollarını
yazılımdan bağımsız kurgular, arıza durumunda sistemin güvenli tarafa düşmesini
varsayılan davranış hâline getiririm.

**İzlenebilir dokümantasyon.** Devreye alma süreçlerini, ölçümleri ve karar
gerekçelerini yazılı tutarım; bir sistemin sürdürülebilirliği onu kuran kişiye
bağımlı olmamalıdır.

**Anlaşılırlık.** Yapay zekâ araçlarını açıkça kullanırım (her depoda
yazılı); teslim ettiğim kodun nasıl çalıştığını açıklayabilir olmayı çalışma
şartı sayarım.

## İletişim

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ahmet-efe-nezli)
[![E-posta](https://img.shields.io/badge/E--posta-24292F?style=flat-square&logo=maildotru&logoColor=white)](mailto:ahmetefenezli@gmail.com)

<sub>Depolarımın bir kısmı aktif yarışma çalışması olduğu için kapalı. Açık
olanlar, üzerinde durabileceğim işlerdir.</sub>
