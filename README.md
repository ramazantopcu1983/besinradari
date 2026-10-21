# BesinRadarı

Uygulama paketli gıda etiketi fotoğrafını tarayıcıda Tesseract.js (Türkçe OCR) ile metne çevirir ve metni seçilen sağlık profilleri/alerjenlerle birlikte sunucu tarafında Groq API'ye göndererek bilgilendirme amaçlı değerlendirir.

## Çalıştırma

- Node.js 18 veya üstünü kurun.
- Groq API anahtarınızı sunucu ortamında `GROQ_API_KEY` olarak ayarlayın. Anahtarı HTML'e, tarayıcı koduna veya Git deposuna eklemeyin. Sohbet veya herkese açık bir yerde paylaşılmış anahtarları iptal edip yenisini oluşturun.
- Windows PowerShell'de:

  ```powershell
  $env:GROQ_API_KEY = "Yeni Groq API anahtarınız"
  npm start
  ```

- Tarayıcıda `http://localhost:3000` adresini açın. OCR kitaplığı ve Türkçe dil verisi ilk kullanımda CDN üzerinden indirilir; internet bağlantısı gerekir.
- İsteğe bağlı olarak `GROQ_MODEL` ve `PORT` ortam değişkenleriyle model/port seçilebilir. Varsayılan model `llama-3.3-70b-versatile`, port `3000`'dir.

## Veri ve sınırlamalar

Etiket fotoğrafı OCR için tarayıcıda işlenir; sunucuya OCR metni ve seçilen profiller gönderilir. Sunucu bu bilgileri değerlendirme için Groq API'ye iletir. API anahtarı yalnızca sunucuda kalır.

OCR hatalı okuyabilir, model yanlış veya eksik değerlendirme yapabilir. Belirsiz ya da okunmayan bilgilerde sonuç belirsiz gösterilir; sonuç tıbbi tavsiye, teşhis veya güvenlik garantisi değildir. Alerji ve sağlık kararlarında ürünün fiziksel ambalajını ve uzman görüşünü esas alın.
