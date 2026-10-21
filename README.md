# BesinRadarı

Uygulama paketli gıda etiketi fotoğraflarını tarayıcıda Tesseract.js (Türkçe ve İngilizce OCR) ile metne çevirir; sıkıştırılmış fotoğrafları ve OCR metnini seçilen sağlık profilleri/alerjenlerle birlikte sunucu tarafında Groq'un görsel anlayabilen modeline göndererek bilgilendirme amaçlı değerlendirir.

Besin tablosunu ve içindekiler/alerjen listesini ayrı, yakın çekim fotoğraflar olarak ekleyin. Kamera ile art arda birden fazla kare alınabilir; galeriden de birden fazla görüntü seçilebilir (en fazla 3; Groq görsel istek sınırı). Fotoğrafların türü model tarafından görüntü ve OCR metninden otomatik sınıflandırılır. Tarayıcı fotoğrafın bir kopyasında gri tonlama, kontrast iyileştirme ve boyut normalizasyonu uygulayıp hem özgün hem iyileştirilmiş görüntüyü OCR'dan geçirir; daha yüksek OCR güven puanına sahip metni kullanır. Görsel analiz için orijinal fotoğraflar ayrıca küçültülüp sıkıştırılır ve Groq'a gönderilir; model görseli OCR metniyle karşılaştırabilir.

## Çalıştırma

- Node.js 18 veya üstünü kurun.
- Groq API anahtarınızı sunucu ortamında `GROQ_API_KEY` olarak ayarlayın. Anahtarı HTML'e, tarayıcı koduna veya Git deposuna eklemeyin. Sohbet veya herkese açık bir yerde paylaşılmış anahtarları iptal edip yenisini oluşturun.
- Windows PowerShell'de:

  ```powershell
  $env:GROQ_API_KEY = "Yeni Groq API anahtarınız"
  npm start
  ```

- Tarayıcıda `http://localhost:3000` adresini açın. OCR kitaplığı ve Türkçe/İngilizce dil verileri ilk kullanımda CDN üzerinden indirilir; internet bağlantısı gerekir.
- İsteğe bağlı olarak `GROQ_VISION_MODEL` ve `PORT` ortam değişkenleriyle model/port seçilebilir. Varsayılan görsel modeli `qwen/qwen3.8-27b`, port `3000`'dir.

## Veri ve sınırlamalar

OCR tarayıcıda çalışır. En fazla 3 adet küçültülmüş etiket fotoğrafı, OCR metni ve seçilen profiller sunucudan Groq API'ye gönderilir. API anahtarı yalnızca sunucuda kalır.

OCR küçük yazı, parlama, eğri ambalaj veya hareket bulanıklığında yine hata yapabilir. İyi ışıkta parlamayı önleyin, kamerayı etikete paralel tutun, yalnızca tablo ya da içerik listesini kadraja doldurun ve odak kilitlenene kadar bekleyin. Analiz sonucundaki OCR metnini ambalajla karşılaştırın.

Görsel analiz için Groq'un `qwen/qwen3.8-27b` modeli kullanılır. API anahtarı olarak `GROQ_API_KEY`, istenirse görsel modelini değiştirmek için `GROQ_VISION_MODEL` ayarlanır; eski `GROQ_MODEL` değişkeni görsel model seçimini etkilemez. Sunucu, model görsel doğrulamayı tamamlamadan veya eksik bilgi varken `UYGUN` döndürürse sonucu `BELIRSIZ` olarak düşürür. Hiçbir AI modeli tıbbi güvenlik garantisi vermez.

OCR hatalı okuyabilir, model yanlış veya eksik değerlendirme yapabilir. Belirsiz ya da okunmayan bilgilerde sonuç belirsiz gösterilir; sonuç tıbbi tavsiye, teşhis veya güvenlik garantisi değildir. Alerji ve sağlık kararlarında ürünün fiziksel ambalajını ve uzman görüşünü esas alın.
