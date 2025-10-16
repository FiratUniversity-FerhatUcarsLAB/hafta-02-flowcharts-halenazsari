modül1
BAŞLA
    Kullanıcıdan TC kimlik numarası ve şifre al
    Kimlik doğrulaması yap
    EĞER kimlik doğrulaması başarısızsa
        "Kimlik bilgileri hatalı!" mesajı göster
        BİTİR
    DEĞİLSE
        Kullanıcıya hastane ve poliklinik listesi göster
        Kullanıcıdan poliklinik seçimi al
        Seçilen polikliniğe uygun doktor listesini getir
        Kullanıcıya doktor listesini göster
        Kullanıcıdan doktor seçimi al
        Seçilen doktorun uygun saatlerini listele
        Kullanıcıdan uygun saat seçimi al
        Randevuyu onayla
        Randevu bilgilerini veri tabanına kaydet
        Kullanıcıya randevu onay mesajı göster
        SMS ile randevu bilgilerini gönder
    SON
BİTİR

modül2
BAŞLA
    Kullanıcıdan TC kimlik numarası ve şifre al
    Kimlik doğrulaması yap
    EĞER kimlik doğrulaması başarısızsa
        "Kimlik bilgileri hatalı!" mesajı göster
        BİTİR
    DEĞİLSE
        Sistemde tahlil sonucu var mı kontrol et
        EĞER sonuçlar henüz hazır değilse
            "Tahlil sonucu hazırlanıyor, lütfen daha sonra tekrar deneyin." mesajı göster
        DEĞİLSE
            Tahlil sonuçlarını görüntüle
            Kullanıcıya PDF olarak indirme seçeneği sun
        SON
    SON
BİTİR
