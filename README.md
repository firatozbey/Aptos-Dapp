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

`presaleMintTime`: satış öncesi basım süresi, beyaz listedeki kullanıcı bundan sonra basabilir. unix zaman damgası 
`presaleMintTime`: satış öncesi basım süresi, beyaz listedeki kullanıcı bundan sonra basabilir. saniye cinsinden unix zaman damgası. https://www.unixtimestamp.com/

`publicMintTime`: genel nane zamanı. saniye cinsinden unix zaman damgası. https://www.unixtimestamp.com/

`whitelistDir`: Beyaz liste dosyasının yolu.

Beyaz liste dosyası, aşağıdaki biçimde bir metin dosyasıdır:

```txt
0x6c4e890a882b013f82a65db9b917a6d285caa892e46f2d93808b56f2aab2dd92 2
0x9d40f83eee59912yatak7488d49becd5274ec21c66c40931c9db95a501e03ecee2 3
0x6c4e890a882b013f82a65db9b917a6d285caa892e46f2d93808b56f2aab2dd92 2
```
her satırın bir cüzdan adresi olmalı ve bu cüzdan beyaz liste aşamasında kaç tane basabilir?
### Candymachine meta verileri
```
     "şeker makinesi": {
         "cmPublicKey": "",
         "cmPrivateKey": ""
     },
```
Devnet veya testnet'te "cmPublicKey" ve "cmPrivateKey" alanlarını boş bırakın, bunlar otomatik olarak oluşturulacak ve finanse edilecektir.
Ana ağda, önce bir hesap oluşturmanız ve ona para göndermeniz gerekir (şeker makinenizi oluşturmak için kullanılır, bu nedenle gazı karşılamak için biraz paranız olduğundan emin olun). Daha sonra hesap adresini ve özel anahtarı dışa aktarmanız ve bunları config.json'a girmeniz gerekir.

### Depolamak
Ürünlerinizi yüklemek için iki seçenek sunuyoruz. Pinata'yı burada örnek olarak kullanacağız. Lütfen arweave'i nasıl kuracağınızı kendiniz araştırın.
```
"depolamak": {
     "çözüm": "pinata",
     "pinata": {
         "pinataApi": "https://api.pinata.cloud/pinning/pinFileToIPFS",
         "pinataPublicKey": "",
         "pinataSecretKey": ""
     },
     "örgü": {
         "keyfilePath": "/Kullanıcılar/Paylaşılan/arweave-keyfile.json"
     }
},
```
Resimlerinizi ve meta verilerinizi ipfs'ye toplu yüklemek için [Pinata](https://www.pinata.cloud/?gclid=CjwKCAjwu5yYBhAjEiwAKXk_eKjm7QEJ2EiRMrXVFVECHFCmRmuHj3btPYzJCxhBLU7XdN0np5vTdBoC6n0QAvD_BwE) kullanacağız. Pinata, NFT görüntülerini ve meta verileri ipfs'ye yüklemek için en çok kullanılan hizmettir.

Bir hesap kaydedin -> sağ üstteki simgeye tıklayın -> API anahtarına tıklayın -> Yeni Anahtar -> pinFileToIPFS'yi etkinleştirin -> genel anahtarınızı ve özel anahtarınızı kopyalayın.

"src" klasörü altındaki "config.json" dosyasını açın (VS kodunu veya başka bir IDE kullanarak).

Pinata tuşlarını ayarlayın.
json
"pinata" :{
"pinataApi": "https://api.pinata.cloud/pinning/pinFileToIPFS",
"pinataPublicKey": "pinata genel anahtarınız"
"pinataSecretKey": "pinata gizli anahtarınız"
}
```

### Ağ değiştir
"constants.py"ye gidin ve "MODE"u "testnet" için "test", "devnet" için "dev" ve "mainnet" için "mainnet" olarak değiştirin.
`candyMachineInfo.js` içindeki modun aynı olarak ayarlandığından emin olun.

### Şeker makinesi oluştur
src klasörü altında çalıştırın
``` bash
python3 cli.py
```
"Şeker makinesi oluştur"u seçin.

***Devnet veya testnet'te bazı apto'ları otomatik olarak şeker makinesi hesabına yatırdık.***

Devnet'te daha fazla aptoya ihtiyacınız varsa, "create_candy_machine.py" içindeki "prepareCandyMachineAccount" hesabına fon sağlamak için "faucet_client" nasıl kullanılacağını kontrol edin. Örnek olarak, bir for döngüsü yazabilirsiniz:
```
aralık(15) içindeki i için:
     musluk_client.fund_account(alice.address(), 100000000)
```

İzin verilen maksimum gas miktarını değiştirmek isterseniz, "constants.py" içinde "MAX_GAS" değerini artırabilirsiniz.

### İlave fonksiyonlar
Satış öncesi basım süresini, genel basım süresini, basım ücretini ve beyaz listeyi güncellemek için seçenekler sunuyoruz. Basitçe `config.json` içindeki değerleri değiştirin ve güncellemek için ilgili komutu çalıştırın.

***Güncelleme WL, geçmiş WL yapılandırmasını geçersiz kılacaktır. Daha fazla wl noktası eklemek istiyorsanız, önceki dosyanın altına ekleyin ve yükleyin.***

### Web sitesi oluştur
npm kurulu olmalıdır, bu basit web sitesini oluşturmak için nextJS kullanıyoruz

"mint-site/helpers/candyMachineInfo.js" içindeki değerleri değiştirin - bu bilgileri config.json'unuzda bulabilirsiniz:

```txt
export const candyMachineAddress = "CM ADRESİNİZ";
export const collectionName = "koleksiyon adı(Büyük/küçük harfe duyarlı!)";
export const collectionCoverUrl = " KAPAK BAĞLANTISI Örn: https://cloudflare-ipfs.com/ipfs/asjdhasjhd";
dışa aktarma sabiti COLLECTION_SIZE = 10
```

mint-site klasörünü aç, çalıştır

``` bash
npm kurulum
```

o zaman koş
``` bash
npm geliştiriciyi çalıştır
```
# Aklı kontrol
1. Her şeyin çalışıp çalışmadığını kontrol etmek için önce örnek görüntüleri ve meta verileri kullanın.
2. Bastırmanın başarılı olup olmadığını kontrol etmek için cli'den test mint işlevini kullanın (tercihen önce devnet ve testnet'te). Test nane, koleksiyonunuzdan BİR nft'yi karıştırmaya çalışacak. Devnet'te program otomatik olarak 3 Aptos bırakacak, testnet ve mainnet'te cm hesabınızda yeterli bakiye olduğundan emin olun.)


# Sorun giderme

1. ERESOURCE_ACCOUNT_EXISTS: Şu anda bir cüzdan bir kaynak hesabı tutabilir, bu normalde ana ağda şekerleme makinesi oluştururken olur ve herhangi bir nedenle (kullanıcı kesintisi veya diğer hatalar) işlem tamamlanmadı. Koleksiyonunuz başarıyla oluşturulduysa, cli menüsünden `Retry failed uploads` seçeneğini deneyin. Aksi takdirde, paranızı yeni bir cüzdana taşıyın ve hesap adresini ve özel anahtarı config.json'a yapıştırın ve yeniden şekerleme makinesi oluşturmayı deneyin.
