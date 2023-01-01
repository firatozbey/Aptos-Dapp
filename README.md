# Aptos

Aptos veya herhangi bir NFT projesine bağlı değilim. Emoji XoX ve Ghost XoX Hariç!!!

- Emoji XoX: https://emojixox.io/
- Ghost XoX: https://ghostxox.com/

# Bu nedir ?

Aptos NFT Mint projesi, içerik oluşturucuların NFT basımı için bir şekerleme makinesi ve Aptos'ta ultra hızlı bir basım web sitesi kurmasına olanak sağlamak için tasarlanmıştır. Şeker makinesi aslen Solana'dandır. Blok zincirindeki genel nft basım sistemine atıfta bulunmak için burada Candy makinesini kullanıyoruz.

Youtube: https://www.youtube.com/channel/UCpqLwqabJb1entJ0pVbFplA

Instagram: https://www.instagram.com/firatozbeys/

Twitter: https://twitter.com/firatozbeys

Sorular için discord: https://discord.gg/zJhuMdN4uS

Aptos hala erken bir aşamada, Elimizden geldiğince çabuk güncelleyeceğiz, ancak sorularınız varsa yardım için discord'umuza gidin.

## Özellikler geliştirildi
* Herkes için başlangıç ve bitiş zamanını ayarlayın.
* Satılacak NFT'leriniz kalmadığında fonlarınızı kabul etmeyecektir.
* Cüzdan tabanlı beyaz liste.
* NFT'niz için telif hakları.
* IPFS'de varlık yükleme.
* Aptos üzerindeki tüm market ve cüzdanlar ile entegredir.
* Entegre cüzdan ve şeker makinenizin durumunun görüntülendiği tamamen özelleştirilebilir web sitesi.

## Hazırlıklar 

### Kod
```sh
git clone https://github.com/firatozbey/Aptos-NFT-Mint.git
```

### Python3
Python sürüm 3.9 ve üstüne ihtiyacınız var.
https://www.python.org/downloads/
### Bağımlılıkları yükleyin
Python sürüm 3.9 ve üstüne ihtiyacınız var

```sh
cd script/third_party
pip3 install -r requirements.txt
```

### nodeJs ve npm
https://docs.npmjs.com/downloading-and-installing-node-js-and-npm
### NFT varlıkları
NFT resmi ve meta verileri oluşturmak için bir dizi çözüm vardır. [HashLips](https://github.com/HashLips/hashlips_art_engine) kullanmanızı öneririz.
Basit ve esnek.

Temel olarak, katmanlı sanata ihtiyacınız var ve görseller ve meta veriler oluşturmak için hashlips kullanıyorsunuz.

İhtiyacımız olan meta veri formatı çok basit. (hashlip'lerden oluşturduğunuz meta veri formatı çalışacaktır, fazladan alanları görmezden geleceğiz.)
Ancak, her meta veri dosyasının farklı, benzersiz bir ada sahip olduğundan emin olun.
```json
{
  "name": "NFT NAME",
  "description": "NFT description",
  "attributes": [
    { "trait_type": "Background", "value": "Black" },
    { "trait_type": "Eyeball", "value": "Red" },
    { "trait_type": "Eye color", "value": "Yellow" },
    { "trait_type": "Iris", "value": "Small" },
    { "trait_type": "Shine", "value": "Shapes" },
    { "trait_type": "Bottom lid", "value": "Low" },
    { "trait_type": "Top lid", "value": "Middle" }
  ]
}
```
Meta verileri oluşturduktan sonra, onu resimlerinizden ayrı bir klasöre koyun. Üst düzey klasörün aşağıdaki gibi oluşturulması gerekir:
```
Assets/  
├─ Images/  
|  |- cover.png
│  ├─ 1.png  
│  ├─ 2.png  
│  ├─ 3.png  
│  ├─ ...  
├─ metadata/  
│  ├─ 1.json  
│  ├─ 2.json  
│  ├─ ...  
```
"cover.png", koleksiyonun kapak resmidir.

**Meta veri ve ilgili resim aynı ada sahip olmalıdır, örneğin: 1.png ve 1.json**
### Aptos cüzdanı
Mainnet ve testnet için [Aptos, testnet'te fon hesabını devre dışı bıraktı], kendi Aptos cüzdanınızı hazırlamalı ve işlem ücretini karşılamak için içine bir miktar para aktarmalısınız.

Martian: https://chrome.google.com/webstore/detail/martian-aptos-wallet/efbglgofoippbgcjepnhiblaibcnclgk

Petra: https://chrome.google.com/webstore/detail/petra-aptos-wallet/ejjladinnckdgjemekebdpeokbikhfci

**Kodumuz meta veri biçimini kontrol edecek, isterseniz kodda devre dışı bırakabilirsiniz**

**Her bir nft için adların (yani, bireysel NFT meta verilerindeki "ad" alanı) benzersiz olduğundan emin olun. Aynı koleksiyonda iki nft aynı ada sahip olamaz. Yinelenen isimleriniz varsa, basım işleminizde sorun olacaktır.**

## Talimatlar

### Koleksiyon meta verileri
```json
"collection": {
    "assetDir": "/Users/Shared/assets/images",
    "metadataDir": "/Users/Shared/assets/metadata",
    "collectionName": "TestCollection101",
    "collectionDescription": "placeholder",
    "collectionCover": "",
    "collectionSize": 10,
    "maxMintPerWallet": 10,
    "mintFee": 100000000,
    "royalty_points_denominator": 1000,
    "royalty_points_numerator": 50,
    "presaleMintTime": 100000000,
    "publicMintTime": 100000000,
    "whitelistDir": "/Users/Shared/assets"
}
```

`assetDir`: Resim klasörünüzün yolu. Hataları önlemek için dosya yolunu manuel olarak girmek yerine doğrudan kopyalayın.

`metadataDir`: Meta veri klasörünüzün yolu. Hataları önlemek için dosya yolunu manuel olarak girmek yerine doğrudan kopyalayın.

`collectionName`: NFT koleksiyon adınız.

`collectionDescription`: NFT açıklamanız.

`collectionCover`: `cover` adlı bir resminiz varsa, bu otomatik olarak doldurulacaktır. Aksi takdirde, kapak resminize bir bağlantı sağlamanız gerekir.

`collectionSize`: NFT koleksiyon boyutunuz.

`maxMintPerWallet`: Cüzdan başına izin verilen mint sayısı.

`mintFee`: 100000000 = 1 APT. örneğin, darphane ücreti olarak 0,5 APT istiyorsanız, 50000000 girin.

"royalty_points_denominator": telif hakkı puanlarının paydası.

"royalty_points_numerator": telif hakkı puanlarının payı.

`presaleMintTime`: satış öncesi basım süresi, beyaz listedeki kullanıcı bundan sonra basabilir. unix zaman damgası i
