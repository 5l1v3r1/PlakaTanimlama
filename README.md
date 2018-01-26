                                                ARAÇ PLAKA TANIMA SİSTEMİ
Projemizde verileri tanıtmak için bir xml dosyası oluşturmak zorundayız. Bu xml dosyası 3 exe den meydana gelmektedir. 
1.Annotation.exe 
2.createsamples.exe 
3.traincascade.exe’dir.
Verileri eğitme aşaması aşağıda anlatılmaktadır.
Öncelikle Annotation.exe’yi oluşturmak için ne hakkında proje yapacaksak onun fotoğraf içerisinde bulunduğu resimler için bir klasör oluşturun ve bu resimleri buraya atın. Şimdilik ihtiyacımız olan şey sadece ne hakkında proje yapacaksak resim sayısını arttırmaktır.(opencv’de pozitif image olarak bilinmektedir.) Unutmayın elimizde ne kadar çok veri varsa o kadar az hataya neden olur , o kadar doğru sonuç döndürür. Denemek için 100 resim bulduğunuzda birde negative yani yapacağınız projedeki nesnenin bulunmadığı fotoğraflara ihtiyacımız vardır. İnternette az bir araştırma ile hazır negative imagelar bulabilirsiniz.(Araç plaka tanıma sistemi için bu imagelar içerisinde plaka olmayan bütün resimlerdir.)
Eğitmeye geldiğimizde ise cmd komutunda bu işlemleri halledebiliriz.
Bilgisayarımızdan cmd komutuna girerek şu kodları sırası ile yazıyoruz.
1.	cd C:\opencv\build\x64\vc12\bin\
(opencv yi nereye kurdu iseniz oranın yolunu kopyalayın ve entera basın.)
2.	opencv_annotation.exe -images (resimlerinizin bulunduğu dosya yolu) 
-annotations oluşturulacak olan textin nereye kayıt edileceği aynı klasör içerisinde oluşturulabilir.)
opencv_annotation.exe -images C:\Users\User\Desktop\car -annotations C:\Users\User\Desktop\car\annotation.txt
       
Biz size anlatmak için Plaka Tanıma üzerinden devam edelim. 2.kodu yazıp entera bastığımız anda karşımızda dosyamızdaki bir resim açılmaktadır. Ne hakkında proje yapıyorsak onu mouseumuz ile seçiyoruz biz burada bize yakın olan plakaları seçmekteyiz.



## ÖNEMLİ
1.	Mouse ile seçmeyi tamamladığımızda “C” tuşuna basarak onaylayabilirsiniz. C tuşuna basıldığı anda yukarıdaki annotation.txt dosyamıza seçtiğimiz yerlerin koordinantları gelmektedir.
2.	“C” ile onayladıktan sonra resim geçişini “N” tuşu ile sağlamaktayız. Bazen belli olmayan fotoğraflar veya seçilemeyen resimler olduğunda “C” tuşuna basmadan “N” ile geçebiliriz.
3.	Yanlış seçtiğimizde ise “ESC” tuşuna basabiliriz.
Tüm resimlere bu işlemi yaptıktan sonra ekran kendiliğinden kapanacaktır dönüp annotation.txt’mize bakabiliriz. İlk açtığınızda resim adınızın önünde resmin dosya yolu yazılı olacaktır. Bu dosya yolunu silmemiz gerekiyor Düzenden değiştir yolu ile toplu olarak Dosya yollarını silebilirsiniz.
      
Annotation.exe’yi bitirdikten sonra sıra CreateSamples.exe’ye geliyor.
CreateSamples için gerekli cmd kodu :
opencv_createsamples.exe -info txt’mizin yolunu yazıyoruz
-num txt içindeki pozitif image sayımız(satır sayısı) 
-vec bir vec dosyası oluşturmak için dosya yolu 
-w dikdörtgenimizin uzun kenar sayısı 
-h dikdörtgenin kısa kenarı
opencv_createsamples.exe -info C:\Users\User\Desktop\Bitirme_Denemeler\car\annotation.txt    -num 100 -vec C:\Users\User\Desktop\Bitirme_Denemeler\car\plaka.vec -w 70 -h 17
Biraz bekleyince klasörümüzde vec dosyası oluşturulmuş olacaktır.
Sıra TrainCascade.exe’mizi oluşturmaya geldi.
TrainCascade için gerekli cmd kodu : 
opencv_traincascade.exe -data oluşacak olan xml’in atılacağı dosya yolu(yeni bir klasör oluşturun)
-vec vec dosyanızın bulunduğu dosya yolu 
-bg negative imageların bulunduğu .txt yolu 
-numPos pozitive image sayısı
-numNeg negative image sayısı(dosya.txt’deki satır sayısı)
-numStages oluşacak olan çerçeve sayısını(hata) en aza indirmek için döngünün kaç kere dönmesi gerektiği 
-minHitRate en düşük isabet oranı
-maxFalseAlarmRate yanlış alarm oranı 
-mem 1024 
-w dikdörtgenimizin uzun kenar sayısı 
-h dikdörtgenin kısa kenarı
opencv_traincascade.exe -data C:\Users\User\Desktop\Bitirme_Denemeler\car\cascade -vec C:\Users\User\Desktop\Bitirme_Denemeler\car\plaka.vec -bg C:\Users\User\Desktop\dosya.txt -numPos 100 -numNeg 350 -numStages 7 -minHitRate 0.995 -maxFalseAlarmRate 0.05 -mem 1024 -w 70 -h 17
Bu işlem biraz zaman alacaktır. Pozitive negative imagelar arttıkça bu zaman dahada artacaktır. Eğer TrainCascade kısmında bazı hatalarla karşılaşıyorsanız dosya.txt’lerdeki dosya yollarınıza dikkat edin.
Hala hataları çözemediyseniz bana mail atarsanız yardımcı olmaya çalışırım. NumStages’i çok abartı sayılar girmeyiniz. Buradaki girilecek değerler önemlidir.
https://docs.opencv.org/3.3.0/dc/d88/tutorial_traincascade.html sayfasını inceleyebilirsiniz.












