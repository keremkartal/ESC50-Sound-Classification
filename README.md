

#  ESC-50 Çevresel Ses Sınıflandırma Projesi

Bu proje, **ESC-50 (Environmental Sound Classification)** verisetini kullanarak çevresel sesleri (insan, hayvan, doğa, şehir vb.) sınıflandırmak amacıyla geliştirilmiş bir Derin Öğrenme (Deep Learning) projesidir.

Proje, ham ses verilerini işleyerek **Log-Mel Spektrogramlara** dönüştürür ve **SpecAugment** tekniği ile veri artırımı (augmentation) uygulayarak modelin başarısını artırmayı hedefler.

##  Veriseti Hakkında

**ESC-50**, 5 ana kategoride toplanmış 50 farklı sınıftan oluşan, her biri 5 saniye uzunluğunda 2.000 adet etiketli ses kaydı içeren bir koleksiyondur.

* **Toplam Kayıt:** 2000 adet (.wav formatında)
* **Süre:** Her kayıt 5 saniye
* **Örnekleme Hızı (Sample Rate):** 44.1 kHz (Projede 22.05 kHz'e düşürülmüştür)
* **Kategoriler:**
    1.  **Doğa Sesleri:** Yağmur, rüzgar, deniz dalgası vb.
    2.  **Hayvan Sesleri:** Köpek, kedi, kuş, kurbağa vb.
    3.  **İnsan Sesleri (Konuşma Dışı):** Ağlama, gülme, öksürme vb.
    4.  **İç Mekan/Ev Sesleri:** Kapı gıcırtısı, cam kırılması, elektrikli süpürge vb.
    5.  **Dış Mekan/Kentsel Sesler:** Siren, korna, motor sesi vb.

##  Kurulum ve Gereksinimler

Projeyi yerel makinenizde veya Google Colab üzerinde çalıştırmak için aşağıdaki Python kütüphanelerine ihtiyacınız vardır:

```bash
pip install numpy pandas librosa matplotlib kagglehub

```

**Kullanılan Temel Kütüphaneler:**

* **Librosa:** Ses işleme ve spektrogram dönüşümleri için.
* **Kagglehub:** Verisetini otomatik indirmek için.
* **Pandas & NumPy:** Veri manipülasyonu ve matris işlemleri için.
* **Matplotlib:** Ses dalgalarını ve spektrogramları görselleştirmek için.

##  Proje Akışı ve Özellikler

Bu notebook (Jupyter Notebook) aşağıdaki adımları içermektedir:

### 1. Veri Edinimi (Data Acquisition)

* `kagglehub` kütüphanesi kullanılarak ESC-50 veriseti doğrudan çalışma ortamına indirilir.
* Dosya dizin yapısı analiz edilir ve gereksiz dosyalar (farklı sample rate kopyaları) temizlenir.

### 2. Ses Ön İşleme (Audio Preprocessing)

Ham ses dosyaları model beslemesi için standardize edilir:

* **Yükleme ve Resampling:** Tüm sesler `22050 Hz` örnekleme hızına dönüştürülür.
* **Süre Sabitleme (Padding/Truncation):** Tüm ses dosyaları tam olarak 5 saniye olacak şekilde ayarlanır. Kısa dosyaların sonuna sessizlik eklenir (padding), uzun dosyalar kırpılır.

### 3. Öznitelik Çıkarımı (Feature Extraction)

Ses dosyaları, CNN (Evrişimli Sinir Ağları) modellerinin işleyebileceği görüntü benzeri formatlara dönüştürülür:

* **Log-Mel Spektrogram:** Ses dalgaları, insan kulağının algısına uygun frekans bantlarına (Mel scale) dönüştürülür ve desibel (dB) ölçeğine çekilir.
* **Parametreler:**
* `n_mels`: 128 (Frekans bandı sayısı)
* `n_fft`: 2048
* `hop_length`: 512



### 4. Veri Artırımı (Data Augmentation - SpecAugment)

Modelin ezberlemesini (overfitting) önlemek için **SpecAugment** tekniği uygulanır:

* **Frekans Maskeleme:** Spektrogram üzerindeki belirli frekans aralıkları rastgele maskelenir.
* **Zaman Maskeleme:** Belirli zaman dilimleri rastgele maskelenir.

##  Görselleştirme

Proje içerisinde her bir işlem adımının çıktısını görebileceğiniz görselleştirmeler mevcuttur:

* Ham ses dalgası (Waveform)
* Dönüştürülmüş Mel-Spektrogram
* Maskeleme uygulanmış (Augmented) Spektrogram

##  Kullanım

Projeyi çalıştırmak için:

1. Repoyu klonlayın veya indirin.
2. `ESC50-Sound-Classification.ipynb` dosyasını Jupyter Notebook veya Google Colab ile açın.
3. Hücreleri sırasıyla çalıştırın. Veriseti otomatik olarak indirilecek ve işlenecektir.

---
