.. _olaylarBolumu:

########################
Olaylar ve Fonksiyonları
########################

Türkçe'de "Ortaya çıkan, oluşan durum" olarak tanımladığımız :index:`olay` (:index:`event`), Kivy için de geçerlidir.
Örneğin  "düğmeye bastırmak", "bastırılmayı bırakmak", "seçim yapmak", "bir tuşa basmak" gibi birçok durum birer 
Kivy olayıdır. Bu olaylar gerçekleştiğinde, programımızın bir tepki vermesi gerekir. Bir olay gerçekleştiğinde verilecek
tepki bir işlev (fonksiyon) tarafından gerçekleştirilebilir. Olay gerçekleştiğinde ilgili fonksiyonun çağrılabilmesi
için, fonksiyonu olaya bağlamak gerekmektedir.

Önce bir düğmeye bastırıldığında üzeirndeki metnin değişmesini sağlayacak bir
program yazmaya çalışalım. Bu programı öncelikle Python kodu yazarak öğreneceğiz, daha sonra ``kvlang`` ile nasıl
gerçekleştirilebileceğine bakacağız. Programımız :numref:`olaylar_main1`'de görülmektedir.

.. literalinclude:: ./programlar/olaylar/1/main.py
    :linenos:
    :tab-width: 4
    :caption: main.py
    :name: olaylar_main1
    :language: python

:numref:`olaylar_main1`'deki programı çalıştırdığımızda tüm ekranı kaplayan bir düğme görünecektir. Düğmenin üzerinde
"Değiştir" metni görünmektedir. Bu düğmeyi ``self``'in bir özelliği yapmamaızın nedeni, sınıf içerisindeki tüm işlevlerden
erişebilmektir. Bu düğmeye bastırıldığında çağrılacak olan işlevi, düğmeinin ``bind()`` özelliği
ile bağlıyoruz. Bir olayı bir nesneye bağlamak için ``bind()`` özelliğini kullanırız. Bu işleve, hangi olayı
bağlamak istiyorsak, onu parametre ve bu parametreye de çağrılacak olan işlevi yazıyoruz. 15. satırda 
``bind()`` işlevine :index:`on_press` parametrisini (bu düğmeye bastırılma olayını ifade eder) ve değer olarak ta
``self.metni_degistir`` işlevini atadık. Böylelikle düğmeye bastırıldığında ``self.metni_degistir`` işlevi çağrılacaktır.
Çağrılan işleve nesnenin kendisi (burada ``self.dugme``'dir) argüman olarak gönderilir. Aslında ``dugme``'yi ``self``'in
özelliği yapmadan, gelen nesne üzerinden de metni değiştirebilirdik:

::

  nesne.text='Tıkladın ve değiştim.'

aynı görevi görürdü. Şimdi aynı programı ``kv lang`` ile yazalım. Programımızı :numref:`olaylar_main2`'da görüyorsunuz.

.. literalinclude:: ./programlar/olaylar/2/main.py
    :linenos:
    :tab-width: 4
    :caption: main.py
    :name: olaylar_main2
    :language: python

İlgili ``kv`` dosyasını :numref:`olaylar_kv2`'da görüyorsunuz.

.. literalinclude:: ./programlar/olaylar/2/olayuyg.kv
    :linenos:
    :tab-width: 4
    :caption: olayuyg.kv
    :name: olaylar_kv2

Şimdi biraz program ve ``kv`` dosyası üzerinde konuşalım. ``kv`` dilinde garfik parçacıklarına isimleri ``id`` özelliği
ile veriyoruz. 3. satırdaki ``id: dugme`` yapmamızın nedeni bu garfik parçacığına (nesneye) program içerisinden ulaşmak için kullanacağımızdır.
Bu düğmeye bastırıldığında çağrılacak olan işlevi ``app``'ın bir özelliği ile veriyoruz. Çağrılan uygulamanın tüm nesneleri,
``kv`` dili içerisinden ``app``'ın özelliği ile erişilir. :numref:`olaylar_main2` programına bakacak olursak, ``kv`` dili 
içerisinde tanımlanmış grafik parçacıklarına erişmek için ``self.root.ids``'nin bir özelliği ile eriştiğimizi anlarsınız. ``kv``'deki
bir nesneye erişmek için o nesnenin ``id`` ile verilmiş ismini kullanıyoruz.

Kullanıcının metin gireceği bir metin kutusu, altında bir etiket ve onun altında da bir düğme bulunan bir program yazalım. Bu programı
yazmadaki amacımız, metin kutusuna girilen değeri etikette görüntülemktir. Programımızı :numref:`olaylar_main3`'da görüyorsunuz.

.. literalinclude:: ./programlar/olaylar/3/main.py
    :linenos:
    :tab-width: 4
    :caption: main.py
    :name: olaylar_main3
    :language: python

Bu programla kullanacağımız ``kv`` dosyasını da :numref:`olaylar_kv3`'da görüyorsunuz.

.. literalinclude:: ./programlar/olaylar/3/olayuyg.kv
    :linenos:
    :tab-width: 4
    :caption: olayuyg.kv
    :name: olaylar_kv3

``kv`` dosyasında etiket için neden ``markup: True`` dediğimizi sonra açaıklayacağız. Programımızı çalıştıralım ve 
üstteki metin kutusuna adımızı yazalım. "Değiştir" düğmesine tıkladığımızda, metin kutusundaki isim etiket üzerine yazılacaktır.
Programın çalışmış halini :numref:`Şekil %s <olaylar1Img>` 'de görüyorsunuz.

.. _olaylar1Img:

.. figure:: ./resimler/olaylar1Img.png

   Girilen metnin etikete yazılması
   
:index:`İşaret Dili` (:index:`markup`)
=======================================

Etiket ve düğmelerde renklerin kullanımı çok kolay.  :numref:`olaylar_kv3`'deki ``kv`` dosyasının 8. satırında ``markup: True``
bulunmaktadır. Bunun anlamı bu etiket metni için işaret dilinin (markup) kullanılacağıdır. Eğer program içerisinde
bir etiket tanımlamış olsaydık, işaret dilini etkinleştirmek için

::

  etiket = Label(markup=True)

diyebilirdik. Ya da daha önceden tanımlanmış bir ``etiket`` nesnesi için:

::

  etiket.markup=True
  
 
şeklinde aktifleştirebilirdik. Keşke Kivy tıpkı Qt gibi standart html'yi desteklemiş olsa idi, ancak ne yazıkki standart
html yerine kendi içerisinde birtakım işaretler vardır. Önce  :numref:`olaylar_main2`'deki programda kullanıcının adını
etikete yazarken kırmızı reknte yazmayı deneyelim. Bunun için 7. satırı aşağıdaki gibi değiştirin:

::
 
  self.root.ids.etiket.text='Merhaba [color=#FF0000] %s [/color] !' % girilen_metin
  
Artık isim kırmızı renkli olacaktır. Burada anlaşılacağı gibi Kivy işaretleri [işaret] ile başlamakta ve
[/işaret] ile bitirlmektedir. Sonucu :numref:`Şekil %s <olaylar2Img>` 'de görüyorsunuz.

.. _olaylar2Img:

.. figure:: ./resimler/olaylar2Img.png

   Etiketlerde renk kullanımı
   
Kullanabileceğimiz diğer işaretler şöyle:

[b][/b]
	Kalın metin
[i][/i]
	İtalik metin
[u][/u]
	Altı çizili metin
[s][/s]
    Üstü çizili metin
[font=<str>][/font]
    Yazıtıpi belirtimi. Örneğin ``[font=DejaVuSerif.ttf]Merhaba Kivy![/font]``
[size=<integer>][/size]
    Yazıtıpi boyutunu belirtir
[color=#<color>][/color]
    Yazı rengini değiştirir
[ref=<str>][/ref]
    Metne bir link (bağ) konulur. Bu bağa tıklandığında "ref" de verilen değer, işleve gönderilir.
[sub][/sub]
    Alt simge olarak gösterilir
[sup][/sup]
    Üst simge olarak gösterilir
    
Basit bir diğer örnek olarak ``ref``'i kullanalım.  :numref:`olaylar_main2`'deki programda etiket üzerindeki metne
tıklandığında ekrana (komut satırına) ``Selam Melike !`` yazacaktır.


.. literalinclude:: ./programlar/olaylar/4/main.py
    :linenos:
    :tab-width: 4
    :caption: main.py
    :name: olaylar_main4
    :language: python


Eğer ``yazdir()`` işlevini şu şekilde değiştirecek olursanız:

::
  
  nesne.text = deger
  
Bu durumda, etiketteki "Merhaba  Fatih !" metine tıkladığınızda, bu metin yerine "Merhaba  Melike !" görünecektir.