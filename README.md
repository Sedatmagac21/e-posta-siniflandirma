# E-posta Sınıflandırma (Naive Bayes)

Bu proje, Naive Bayes algoritmasını kullanarak e-postaları spam veya spam olmayan (ham) olarak sınıflandırmayı amaçlamaktadır. Proje, temel doğal dil işleme (NLP) adımlarını ve sıfırdan bir Naive Bayes sınıflandırıcısının implementasyonunu içermektedir. Ayrıca, sayısal kararlılığı artırmak için logaritmik olasılıklar kullanan bir versiyon da içerir.

## İçindekiler

- [Proje Açıklaması](#proje-açıklaması)
- [Kullanılan Teknolojiler](#kullanılan-teknolojiler)
- [Kurulum](#kurulum)
- [Kullanım](#kullanım)
- [Veri Seti](#veri-seti)
- [Modelin Performansı](#modelin-performansı)
- [Logaritmik Olasılıklar](#logaritmik-olasılıklar)
- [Değerlendirme Metrikleri](#değerlendirme-metrikleri)
- [Katkıda Bulunma](#katkıda-bulunma)

## Proje Açıklaması

Bu proje, e-posta içeriğini analiz etmek ve bu e-postaların spam olup olmadığını tahmin etmek için Naive Bayes sınıflandırma algoritmasını kullanır. Proje aşağıdaki adımları içerir:

1.  **Veri Ön İşleme:** E-posta metinlerinden "Konu:" önekini kaldırma, metni küçük harfe çevirme, noktalama işaretlerini ve İngilizce stop word'lerini (durak kelimeleri) temizleme.
2.  **Veri Bölme:** Veri setini eğitim ve test kümelerine ayırma (80% eğitim, 20% test).
3.  **Kelime Frekansı Hesaplama:** Eğitim verilerindeki her kelimenin spam ve ham e-postalarda görülme sıklığını hesaplama (Laplace düzeltmesi ile).
4.  **Sınıf Olasılıkları Hesaplama:** Spam ve ham e-postaların eğitim veri setindeki oranlarını belirleme.
5.  **Naive Bayes Sınıflandırıcısı:** Eğitilen frekanslar ve olasılıklar kullanarak yeni e-postaların spam veya ham olarak sınıflandırılması.
6.  **Logaritmik Naive Bayes Sınıflandırıcısı:** Olasılıkların çarpımı yerine logaritmaların toplamını kullanarak sayısal kararlılığı artıran bir alternatif implementasyon.
7.  **Model Değerlendirme:** Test veri seti üzerinde doğruluk (accuracy), geri çağırma (recall) ve kesinlik (precision) gibi metriklerle modelin performansını değerlendirme.

## Kullanılan Teknolojiler

* **Python:** Temel programlama dili.
* **NumPy:** Diziler ve matematiksel işlemler için.
* **Pandas:** Veri manipülasyonu ve analizi için.
* **NLTK (Natural Language Toolkit):** Stop word'leri kaldırmak ve metin işleme için.
* **scikit-learn (sklearn):** Metin özellik çıkarımı için (`ENGLISH_STOP_WORDS`).
* **re (Regular Expression):** Metin temizleme için.
* **sys:** Sistemle ilgili bilgiler için (`sys.float_info`).

## Kurulum

1.  Bu depoyu GitHub üzerinden klonlayın:
    ```bash
    git clone <bu_deponun_github_adresi>
    cd <depo_adı>
    ```

2.  Gerekli kütüphaneleri yükleyin:
    ```bash
    pip install numpy pandas nltk scikit-learn
    ```

3.  NLTK kütüphanesi için gerekli veri kümelerini indirin:
    ```python
    import nltk
    nltk.download('stopwords')
    nltk.download('punkt')
    ```

## Kullanım

1.  Proje dizininde, ana Python dosyalarını çalıştırın (genellikle sırayla veya tek bir ana dosya üzerinden):

2.  Kod, e-posta verilerini yükleyecek, ön işleyecek, veri setini eğitim ve test kümelerine bölecek, modelleri (standart ve logaritmik Naive Bayes) eğitecek ve test veri seti üzerinde performanslarını değerlendirecektir.

3.  Projenin son bölümlerinde, örnek e-postaların nasıl sınıflandırıldığı ve her iki modelin olasılık (veya logaritmik olasılık) çıktıları gösterilmektedir.

## Veri Seti

* Bu proje, e-posta verilerini içeren bir CSV dosyası (`emails.csv`) kullanmaktadır.
* CSV dosyası, e-posta içeriğini içeren bir 'text' sütunu ve e-postanın spam (1) veya ham (0) olup olmadığını belirten bir 'spam' sütunu içermelidir.
* Veri seti, eğitim ve test kümelerine ayrılmadan önce karıştırılır.
* Veri setinin nasıl elde edildiğine dair ek bilgileri buraya ekleyebilirsiniz (örneğin, bir kamu veri setinden veya kendi topladığınız verilerden).

## Modelin Performansı

Proje, hem standart hem de logaritmik Naive Bayes algoritmalarını kullanarak e-postaları sınıflandırır. Test veri seti üzerinde elde edilen performans metrikleri şunlardır:

**Standart Naive Bayes:**
*** Doğruluk: 0.8613 ***

**Logaritmik Naive Bayes:**
*** Doğruluk: 0.9842 ***



Model, test veri setindeki e-postaların doğru sınıflandırılmasında bu oranlarda başarı göstermiştir. Geri çağırma, spam e-postaların ne kadarının doğru tespit edildiğini gösterirken, kesinlik ise pozitif olarak tahmin edilen e-postaların ne kadarının gerçekten spam olduğunu gösterir.

## Logaritmik Olasılıklar

Projede, standart olasılıkların çarpımı yerine logaritmik olasılıkların toplamını kullanan bir Naive Bayes implementasyonu bulunmaktadır. Bu yaklaşım, çok küçük olasılıkların çarpılması sonucu ortaya çıkabilecek sayısal kararsızlıkları önlemeye yardımcı olur. Logaritma, çarpma işlemini toplama işlemine dönüştürerek bu tür sorunların önüne geçer.

## Değerlendirme Metrikleri

Modelin performansını değerlendirmek için aşağıdaki metrikler kullanılmıştır:

* **Doğruluk (Accuracy):** Toplam doğru tahminlerin tüm tahminlere oranı.
* **Geri Çağırma (Recall):** Gerçek spam e-postaların ne kadarının model tarafından doğru bir şekilde spam olarak sınıflandırıldığı.
* **Kesinlik (Precision):** Modelin spam olarak sınıflandırdığı e-postaların ne kadarının gerçekten spam olduğu.
* **Yanlış Pozitif (False Positive):** Modelin yanlışlıkla spam olarak etiketlediği ham e-postaların sayısı.

## Katkıda Bulunma

Bu projeye katkıda bulunmak isterseniz, lütfen aşağıdaki adımları izleyin:

1.  Projeyi fork edin.
2.  Kendi branch'inizi oluşturun (`git checkout -b feature/yeni-ozellik`).
3.  Yaptığınız değişiklikleri commit edin (`git commit -am 'Yeni özellik eklendi'`).
4.  Branch'inizi push edin (`git push origin feature/yeni-ozellik`).
5.  Pull request oluşturun.



**Ek Notlar:**

* Projedeki veri ön işleme adımları (örneğin, stop word'lerin kaldırılması, tokenleştirme) NLTK kütüphanesi kullanılarak gerçekleştirilmiştir.
* Hem standart hem de logaritmik Naive Bayes sınıflandırıcıları, kelime frekansları ve sınıf olasılıkları temel alınarak sıfırdan implemente edilmiştir.
* Modelin performansı, kullanılan veri setinin büyüklüğüne ve içeriğine bağlı olarak değişebilir. Logaritmik yaklaşım, özellikle çok sayıda kelime içeren e-postalarda sayısal kararlılık açısından avantaj sağlayabilir.

Bu güncellenmiş README dosyası, projenizin tüm yönlerini ve implementasyon detaylarını kapsamaktadır. GitHub deponuzdaki README.md dosyasına bu içeriği kopyalayıp kullanabilirsiniz. Elde ettiğiniz gerçek performans metriklerini ([elde_edilen_doğruluk_değeri] vb.) ilgili yerlere eklemeyi unutmayın. Başarılar dilerim!
