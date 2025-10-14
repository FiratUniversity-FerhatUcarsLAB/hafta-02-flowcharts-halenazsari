BAŞLA
  tanımla bakiye = 2000
  tanımla günlük_limit = 1500
  tanımla deneme_hakkı = 3
  tanımla doğru_pin = 1234

  // PIN DOĞRULAMA
  DÖNGÜ (deneme_hakkı > 0)
      OKU girilen_pin
      EĞER girilen_pin == doğru_pin İSE
          YAZ "PIN doğru. İşleme devam ediliyor..."
          ÇIK DÖNGÜDEN
      DEĞİLSE
          deneme_hakkı = deneme_hakkı - 1
          YAZ "Hatalı PIN. Kalan deneme hakkı: ", deneme_hakkı
      BİTİR EĞER
  SON DÖNGÜ

  EĞER deneme_hakkı == 0 İSE
      YAZ "Hesap kilitlendi."
      DUR
  BİTİR EĞER

  // PARA ÇEKME İŞLEMİ
  TEKRARLA
      OKU tutar
      EĞER tutar % 20 != 0 İSE
          YAZ "Tutar 20 TL katlarında olmalı."
      DEĞİLSE EĞER tutar > bakiye İSE
          YAZ "Yetersiz bakiye."
      DEĞİLSE EĞER tutar > günlük_limit İSE
          YAZ "Günlük limit aşıldı."
      DEĞİLSE
          bakiye = bakiye - tutar
          günlük_limit = günlük_limit - tutar
          YAZ tutar, " TL çekildi. Yeni bakiye: ", bakiye
      BİTİR EĞER

      YAZ "Başka işlem yapmak ister misiniz? (E/H)"
      OKU cevap
  KENARCA cevap == "E"
  YAZ "İyi günler dileriz."
BİTİR
