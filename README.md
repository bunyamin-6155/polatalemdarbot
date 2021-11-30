# Polat Alemdar
Bir sqlalchemy veritabanı ile python3 üzerinde çalışan modüler bir telgraf Python botu..

Başlangıçta çoklu yönetici özelliklerine sahip basit bir grup yönetimi botu, gelişti, son derece modüler ve kullanımı basit hale geldi.

Telegramda [Polat Alemdar](https://t.me/polat_alemdarbot).
Marie ve ben, botunuzu kurmak için yardım isteyebileceğiniz, yeni özellikler keşfedebileceğiniz/talep edebileceğiniz, hataları bildirebileceğiniz ve yeni bir güncelleme olduğunda döngüde kalabileceğiniz bir [destek kanalı](https://t.me/polatalemdarbothaberler) yönetiyoruz, Elbette bir veritabanı şeması değiştiğinde ve bazı tablo sütunlarının değiştirilmesi/eklenmesi gerektiğinde de yardımcı olacağım. Bakımcılara, tüm şema değişikliklerinin taahhüt mesajlarında bulunacağını ve yeni taahhütleri okuma sorumluluklarının olduğunu unutmayın.

duyurular ve haberlerden bilgiliniz olması için [KANAL](https://t.me/polatalemdarbothaberler)

telegram da ben da babba [Bünyo](https://t.me/bunyamin6155)!

## Doğrudan Heroku'ya dağıtmak için aşağıdaki Heroku'ya Dağıt düğmesine de dokunabilirsiniz!

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/bunyamin-6155/polatalemdarbot)

## Botu başlatmak.

Veritabanınızı kurduktan ve yapılandırmanız (aşağıya bakın) tamamlandıktan sonra, çalıştırmanız yeterlidir:

`python3 -m tg_bot`


## Botu kurma (Kullanmayı denemeden önce bunu okuyun!):
Lütfen python3.6 kullandığınızdan emin olun, çünkü her şeyin eski python sürümlerinde beklendiği gibi çalışacağını garanti edemem! Bunun nedeni, işaretleme ayrıştırmasının varsayılan olarak 3.6'da sıralanan bir dict üzerinden yinelenerek yapılmasıdır.

### Yapılandırma

Botunuzu yapılandırmanın iki olası yolu vardır: bir config.py dosyası veya ENV değişkenleri.

Tercih edilen sürüm `config.py`tüm ayarlarınızı bir arada gruplanmış olarak görmeyi kolaylaştırdığından bir dosya kullanmaktır .
Bu dosya `tg_bot` , `__main__.py` dosyanın yanında klasörünüze yerleştirilmelidir .  
Burası, bot simgenizin yanı sıra veritabanı URI'niz (bir veritabanı kullanıyorsanız) ve diğer ayarlarınızın çoğunun yükleneceği yerdir.

sample_config dosyasını içe aktarmanız ve Config sınıfını genişletmeniz önerilir, çünkü bu, yapılandırmanızın
sample_config içinde ayarlanan tüm varsayılanları içermesini sağlayacak ve böylece yükseltmeyi kolaylaştıracaktır.

Bir örnek `config.py` dosyası olabilir:
```
from tg_bot.sample_config import Config


class Development(Config):
    OWNER_ID = 1193178307  # benim telegram ID
    OWNER_USERNAME = "bunyamin6155"  # benim telegram kullanıcı adı
    API_KEY = "your bot api key"  # benim api key,botfather'ın verdiği
    SQLALCHEMY_DATABASE_URI = 'postgresql://username:password@localhost:5432/database'  # database kimlik bilgileri
    MESSAGE_DUMP = '-1234567890' # botun üye olduğu grup id'si
    USE_MESSAGE_DUMP = True
    SUDO_USERS = [18673980, 83489514]  # Bot'a sudo erişimi olan kullanıcıların id listesi.
    LOAD = []
    NO_LOAD = ['translation']
```

Bir config.py dosyanız yoksa (heroku'da örnek), ortam değişkenlerini kullanmak da mümkündür.
Aşağıdaki env değişkenleri desteklenir:
 - `ENV`:Bunu HERHANGİ BİR ŞEY olarak ayarlamak env değişkenlerini etkinleştirir

 - `TOKEN`: Bu senin bot token'in.
 - `OWNER_ID`: Bot sahibinin id'si
 - `OWNER_USERNAME`: Bot sahibinin kullanıcı adı

 - `DATABASE_URL`: Senin database url
 - `MESSAGE_DUMP`: isteğe bağlı: insanların eski mesajlarını silmesini önlemek için yanıtladığınız kayıtlı mesajlarınızın saklandığı bir sohbet
 - `LOAD`:  Yüklemek istediğiniz modüllerin boşlukla ayrılmış listesi
 - `NO_LOAD`: Yüklemek istemediğiniz modüllerin boşlukla ayrılmış listesi
 - `WEBHOOK`: Bunu HERHANGİ BİR ŞEY olarak ayarlamak, env modundaki mesajlarda web kancalarını etkinleştirir
 - 
 - `URL`: Web kancanızın bağlanması gereken URL (yalnızca web kancası modu için gereklidir)

 - `SUDO_USERS`: Sudo kullanıcıları olarak düşünülmesi gereken, boşlukla ayrılmış kullanıcı id'leri listesi
 - `SUPPORT_USERS`:Destek kullanıcıları olarak kabul edilmesi gereken, boşlukla ayrılmış bir kullanıcı id'leri listesi (gban/ungban olabilir, başka bir şey değil)
 - `WHITELIST_USERS`: Beyaz listeye alınmış olarak kabul edilmesi gereken, boşlukla ayrılmış bir kullanıcı id listesi - yasaklanamazlar.
 - `DONATION_LINK`: İsteğe bağlı: Bağış almak istediğiniz bağlantı.
 - `CERT_PATH`: Web kancası sertifikanızın yolu
 - `PORT`: Web kancalarınız için kullanılacak bağlantı noktası
 - `DEL_CMDS`: Bu komutu kullanma haklarına sahip olmayan kullanıcılardan komutların silinip silinmeyeceği
 - `STRICT_GBAN`: Eski grupların yanı sıra yeni gruplarda da gban'ları zorunlu kılın. Gbanlı bir kullanıcı konuştuğunda banlanır.
 - `WORKERS`: Kullanılacak iş parçacığı sayısı. 8, önerilen (ve varsayılan) miktardır, ancak deneyiminiz değişebilir. __Not__ daha iplikle çıldırıyor mutlaka SQL veri erişimlerin büyük miktarda ve yolu piton asenkron çağrılar eser verilmiş, bot hızlandırmak alışkanlık olduğunu..
 - `BAN_STICKER`:  Kişileri yasaklarken hangi çıkartmanın kullanılacağı.
 - `ALLOW_EXCL`: Ünlem işareti kullanımına izin verilip verilmeyeceği ! komutların yanı sıra /.

### Python bağımlılıkları

Proje dizinine gidip aşağıdakileri çalıştırarak gerekli python bağımlılıklarını kurun:

`pip3 install -r requirements.txt`.

Bu, gerekli tüm python paketlerini kuracaktır.

### Database

Veritabanına bağlı bir modül kullanmak istiyorsanız (örneğin: kilitler, notlar, kullanıcı bilgileri, kullanıcılar, filtreler, karşılamalar),
sisteminizde bir veritabanının kurulu olması gerekir. Postgres kullanıyorum, bu yüzden optimum uyumluluk için kullanmanızı tavsiye ederim.

Postgres durumunda, bir debian/ubuntu sisteminde bir veritabanını bu şekilde kurarsınız. Diğer dağıtımlar değişebilir.

- postgresql'i kurun:

`sudo apt-get update && sudo apt-get install postgresql`

- postgres kullanıcısına değiştirin:

`sudo su - postgres`

- yeni bir veritabanı tablosu oluşturun:(Uygun şekilde kullanıcı adı yapın):

`createuser -P -s -e YOUR_USER`

Bunu, şifrenizi girmeniz gerekerek izleyecektir.

- Yeni bir veritabanı oluşturun:

`createdb -O YOUR_USER YOUR_DB_NAME`

Kullanıcı adı ve veritabanı adınızı uygun şekilde değşitirin

- Sonunda:

`psql YOUR_DB_NAME -h YOUR_HOST YOUR_USER`

Bu, terminaliniz aracılığıyla veritabanınıza bağlanmanıza izin verecektir.
 Varsayılan olarak, YOUR_HOST 0.0.0.0:5432 olmalıdır.

Artık veritabanı URI'nizi oluşturabilmelisiniz. Bu olacak:

`sqldbtype://username:pw@hostname:port/db_name`

Sqldbtype'ı kullandığınız db ile değiştirin (örneğin postgres, mysql, sqllite, vb.) kullanıcı adınız, parolanız, ana bilgisayar adı (localhost?), bağlantı noktası (5432?) ve db adı için tekrarlayın.

## Modüller
### Yükleme Sırası Ayarlama.
Modül yükleme sırası `LOAD` ve `NO_LOAD` konfigürasyon ayarları aracılığıyla değiştirilebilir.
Bunların her ikisi de listeleri temsil etmelidir.

Eğer `LOAD` boş bir liste ise, tüm modüller `modules/` tüm modüller varsayılan olarak yüklenmesi için seçilecektir.

If `NO_LOAD` is not present, or is an empty list, all modules selected for loading will be loaded.

If a module is in both `LOAD` and `NO_LOAD`, the module will not be loaded - `NO_LOAD` takes priority.

### Creating your own modules.

Creating a module has been simplified as much as possible - but do not hesitate to suggest further simplification.

All that is needed is that your .py file be in the modules folder.

To add commands, make sure to import the dispatcher via

`from tg_bot import dispatcher`.

You can then add commands using the usual

`dispatcher.add_handler()`.

Assigning the `__help__` variable to a string describing this modules' available
commands will allow the bot to load it and add the documentation for
your module to the `/help` command. Setting the `__mod_name__` variable will also allow you to use a nicer, user
friendly name for a module.

The `__migrate__()` function is used for migrating chats - when a chat is upgraded to a supergroup, the ID changes, so 
it is necessary to migrate it in the db.

The `__stats__()` function is for retrieving module statistics, eg number of users, number of chats. This is accessed 
through the `/stats` command, which is only available to the bot owner.
