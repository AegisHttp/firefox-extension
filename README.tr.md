# Aegis Http GPG Login (Mozilla Firefox) | TR / [EN](README.md)

![Logo](icons/logo.png)

Aegis Http, web uygulamalarınızın gönderdiği veri trafiğini (POST, PUT vb.) arka planda tamamen şeffaf ve otonom bir şekilde PGP kullanarak şifreleyen bir Uçtan Uca Şifrelemeli (E2E) Mozilla Firefox uzantısıdır. Frontend (Angular, React, Vue vb.) kodlarınızda herhangi bir şifreleme mantığı kullanmadan veri trafiğini güvence altına alır.

## Özellikler

- **Şeffaf Yakalama:** `XMLHttpRequest` çağrılarını otomatik yakalar ve araya girer. Frontend geliştiricilerinin projesinde extra PGP paketi kullanmasına gerek yoktur.
- **Ayrıştırılmış Güvenlik (Native Messaging):** PGP özel anahtarınız (Private Key) asla JavaScript belleğine çekilmez ve tarayıcıya girmez. Firefox taraflı olan bu eklenti, Mozilla'nın yerleşik _Native Messaging_ köprüsüyle arka planda çalışan Rust servisinizle konuşur.
- **Otonom Çözme:** Çıkan şifreli izlere dönen sunucu yanıtları da PGP şifreli geldiğinde; bu eklenti otomatik olarak yerel köprüden deşifre eder ve sayfanıza ham JSON verisini iade eder.

## Kurulum

1. Firefox tarayıcınızdan `about:debugging#/runtime/this-firefox` sekmesine (sayfasına) gidin.
2. "Geçici Eklentiler (Temporary Extensions)" altında, **Geçici Eklenti Yükle (Load Temporary Add-on...)** butonuna tıklayın.
3. `/firefox-extension` içindeki `manifest.json` dosyasını seçin.
4. **DİKKAT! Native Host daemon servisinizin kurulduğundan emin olun!** Aksi takdirde, uzantınız arka plandaki GPG servisine mesaj gönderemez. Eğer hata alırsanız Rust manifestinizin `~/.mozilla/native-messaging-hosts/aegis-http.json` dizininde olduğundan emin olun. (Daha fazla bilgi için ana proje Readme sine göz atın)

## Klasör Yapısı

- `manifest.json`: Firefox kimliğini tanımlayan (Gecko ID v.b) eklenti ayar dosyası.
- `background.js`: Content script'leri ve Rust tabanlı yerel API arasında çift yönlü haberleşmeyi sağlayan background dosyası.
- `content.js`: Yetkili sitelerde `inject.js` komut setini site DOM'una izole olmayan şekilde enjekte eder.
- `inject.js`: Tarayıcınızdaki `XMLHttpRequest.prototype` işlevlerini ezen, yüksek ayrıcalıklı Proxy/Interceptor dosyasıdır.
- `icons/`: Tarayıcı eklentisindeki UI gösterimleri için optimize edilmiş marka ikonları.
