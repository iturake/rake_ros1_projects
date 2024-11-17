![](media/image2.png){width="3.0902777777777777in"
height="0.9861111111111112in"}

![](media/image3.png){width="1.2655741469816273in"
height="0.983439413823272in"}

**İstanbul Teknik Üniversitesi Robotik Arama Kurtarma Ekibi**

**Görev Raporu**

**Görev Konusu:** ROS Proje Ödevi

**Hazırlayan:** Önder İhsan Kul

**Tarih:** 15.11.2024

**Proje Amacı**

İTÜ RAKE takımına alınmış yeni üyelerin kurs süreçlerinin ardından
öğrendiği konseptleri uygulayarak pekiştirmelerini, robotik bir projeyi
parçaları ile kurgulama becerilerini geliştirmelerini ve takımın
projelerine katkı vermek için gereken altyapıyı edinmelerini sağlamak.

**Proje Açıklaması**

Yapılması istenen proje, arama kurtarma operasyonlarında aktif olarak
kullanılan bir alt sürecin ROS ve Gazebo kullanılarak simülasyonudur.
Projemiz bir arama projesidir. Projede bir Gazebo dünyasında 4 farklı
rastgele seçilmiş konumda bulunan insanı, gps olarak konumları ve
bulundukları yerde çekilmiş fotoğrafları ile bir ROS topic' inde
depolamak amaçlanmaktadır. Bu projeyi yaparken üyelerimiz; Gazebo
pluginlerini kullanmayı, kendileri custom topic oluşturmayı, robotik bir
sistemi ROS'ta tasarlamayı, sensör verilerini işleyip bu verilere
dayanarak belirli fonksiyonları tetiklemeyi uygulamalı olarak
göreceklerdir. Projenin teknik detayları aşağıda açıklanmıştır.

**Proje Teknik Detayları**

1.  Projede kullanacağınız kaynaklar \<repo_link\> adlı github reposunda
    > bulunmaktadır.

2.  Projenizde diferansiyel sürüş sistemine sahip bir bir robotu
    > kullanacaksınız. Kullanacağınız robotun urdf dosyaları ve urdf
    > dosyalarında kullanılacak mesh dosyaları proje reposunda
    > verilmiştir.

- Bu dosyaları workspace'inize ekledikten sonra Rviz üzerinde
  > aşağıdakine benzer bir görüntü almanız gerekmektedir.

![](media/image5.png){width="4.651042213473316in"
height="2.4336843832021in"}

3.  Projenizi rastgele 4 konumda bulunan insanlar içeren bir gazebo
    > dünyasında gerçekleştireceksiniz. kullanacağınız world dosyası
    > linkteki repoda bulunan testworld.sdf adlı dosyadır.

4.  Robotunuzu klavyede PgUp, PgDn, PgLeft, PgRight ok tuşları ile
    > kontrol edeceksiniz, kontrol komutunu topic olarak publishlemek
    > için key_teleop ros kütüphanesini kullanacaksınız

- istenilen konfigürasyon, ileri ok tuşu: +0.7 doğrusal hız, geri ok
  > tuşu: -0.7 doğrusal hız, sol ok tuşu: +0.4 açısal hız, sağ ok tuşu:
  > -0.4 açısal hız

  a.  key_teleop kütüphanesini kullanarak hangi ok komutuna karşılık
      > nasıl doğrusal ve açısal olarak nasıl bir hız değişimi olduğunu
      > gözlemleyin.

  b.  Klavye komutlarını istenilen hız komutlarına dönüştürebilmek için
      > /bumper_bot_controller/cmd_vel adında yeni bir topic e
      > publishlemek üzere key_teleop tarafından ilk kontrol komutunun
      > yayınlandığı mesaja subscribe olan bir node yazın

  c.  Bu node içerisinde subscribe olduğunuz kontrol komutunda
      > değişiklikler yapıp yeni /bumper_bot/cmd_vel topic'ine
      > değiştirilmiş mesajı publishleyin.

5.  robotunuzun jointlerini -wheel_left_link, wheel_right_link- kontrol
    > etmek, onlara hız komutları göndermek için 4. adımda yazdığınız
    > /bumper_bot_controller/cmd_vel topic ini alarak bu hız komutunu
    > joint hız komutlarına çeviren ve bu komutu joint_state mesajı
    > olarak yayınlayan node'u yazacaksınız

    a.  öncelikle kullanacağınız joint_velocity_state_controller için
        > bir config(.yaml) dosyası yazmanız gerekmektedir.

- [[http://wiki.ros.org/ros_control]{.underline}](http://wiki.ros.org/ros_control)
  > linkinden projenize uygun kontrolcüyü seçin

- Ardından internet üzerinde bir araştırma yaparak aracınızı her bir
  > tekerleğe hız vererek sürebilmek için bir config(.yaml) dosyası
  > yazın

  a.  Kontrolcülerinizi config dosyaları ile launchlamak için bir
      > .launch dosyası yazın.

<!-- -->

- controller.launch dosyanızı yazmak için internet üzerinden araştırma
  > yapınız.

6.  Joint-control bölümünün çalışırlığından emin olmanızın ardından
    > aracınızın urdf dosyasında aracın ön tarafına front_camera_link
    > adında bir link ve bu linkle base_link arasında sabit(fixed) joint
    > ekleyin.(sabit joint in xyz rpy değerlerini ve kameranın en, boy,
    > yükseklik değerlerini elle ayarlayınız.)

7.  kameranızı işlevsel hale getirmek için gazebo kamera pluginini ana
    > urdf dosyanıza ekleyin ve front_camera_link için gerekli
    > parametreleri tanımlayın.

- Bu adımda hazırda kamera kullanmakta olan robotların urdf dosyalarını
  > incelemek akıllıca olacaktır.

- Bu adımın ardından kameranızın aldığı görüntüyü bir
  > /bumper_bot/front_camera\* namespace i altındaki rostopicleri
  > üzerinden görüntüleyebiliyor olmanız gerekmektedir.

- plugin i tanımlarken "visualize" tag ini true olarak ayarlamanız
  > debugging süreçlerinde yardımcı olacaktır.

- publish_frequency parametresini 10 olarak ayarlayın

- diğer parametreleri bulduğunuz örneklerdeki değerlere göre
  > tanımlayabilirsiniz.,

Plugin Eklemesinin ardından aşağıda gösterilen aracımız Umay'ın arayüzü
üzerinde gördüğünüze benzer kamera görüntüleri alabiliyor olmanız
gerekmektedir.

![](media/image4.png){width="4.963542213473316in"
height="2.6384273840769903in"}

8.  Ardından GPS sensörünü simüle edebilmek için internet üzerinden
    > araştırma yaparak robotunuzun urdf dosyasına bir gps sensörü
    > ekleyiniz.

- Bu aşamada da aracınız üzerinde gps_link adında bir link tanımlayıp
  > gazebo pluginine bu linki parametre olarak vereceksiniz.

<!-- -->

- Bu aşamanın ardından aracınızın GPS sensör verisini
  > /bumper_bot/gps/fix adlı topic te görebiliyor olmanız gerekmektedir.

9.  Şimdi de uygulamada kullanmak üzere kendiniz birkaç topic
    > tanımlamanız gerekmektedir.

<!-- -->

a.  WoundedInfo adında, simülasyonda bulduğunuz insanların fotoğraf ve
    > anlık gps konumunu içerecek custom message ı tanımlayınız.

- İçeriği

  - sensor_msgs/NavSatFix gps-\>anlık konum bilgileri için

    - time_stamp

    - latitude

    - longitude

bilgileri bu alt-başlıkta doldurulacak.

- sensor_msgs/Image img-\>yaralının görüldüğü anın YOLOv8 ile işlenmiş
  > fotoğrafı(raw kamera görüntüsü değil, işlenmiş görüntü
  > kullanılacak.)

  - bu topic e alt topic'te 372x372 boyutunda fotoğraflar
    > bulundurulmalıdır.

b.  WoundedInfoArray

> Yukarıda verilen WoundedInfo topic inden birçok objeyi bulunduran bir
> array oluşturulacak

- WoundedInfo wounded_array\[\]

> 10\. Bu adımda Görüntü işleme işlemleri için OpenCV ve ROS arasındaki
> etkileşimi sağlayabilmek adına cv_bridge paketini kullanacak, verilen
> görüntülerdeki insanları algılamak için YOLOv8'den faydalanacak ve
> işlediğiniz görüntülerde insan resmi bulunup bulunmadığına göre
> çeşitli işlemler gerçekleştireceksiniz.

a.  Tanımladığınız kamera topic'ine subscribe olan, aldığı görüntüleri
    > görsellere çeviren, çevirdiği görselleri yolov8 modeline işleten,
    > bunun ardından verilen görüntüde insan bulunma yüzdesi %75'ten
    > büyükse çeşitli işlemler yapacak şekilde bir node taslağı
    > oluşturun.

b.  Yazdığınız node'u her alınan görsel değeri için insan bulunma
    > tahmininin doğruluk yüzdesi %75'ten büyükse görüntünün algılandığı
    > andaki zaman verisini, gps verisini ve çekilen görüntüyü
    > WoundedInfo tipindeki bir mesaja çevirecek, ardından bu mesajı
    > WoundedInfoArray tipinde bir topic in wounded_array elemanına
    > ekleyecek şekilde güncelleyin.

c.  Yolov8 modelinin tahmininin %75'ten büyük olmaması durumunda node'un
    > bir işlem gerçekleştirmesine gerek yoktur.

- Yolov8'i internette bulacağınız hazır paketlerle veya orijinal
  > reposundan robotunuza entegre edebilirsiniz

11\. Tüm alt bölümleri tamamlamanızın ardından alt bölümleri tek bir
dosya altında launchlayacak bir .launch dosyası yazın.
