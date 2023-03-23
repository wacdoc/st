# Iketsetse seva ea hau ea ho romella mangolo a SMTP

## ketapele

SMTP e ka reka litšebeletso ka kotloloho ho barekisi ba maru, joalo ka:

* [Amazon SES SMTP](https://docs.aws.amazon.com/ses/latest/dg/send-email-smtp.html)
* [Ali cloud email push](https://www.alibabacloud.com/help/directmail/latest/three-mail-sending-methods)

U ka boela ua iketsetsa seva ea hau ea mangolo - ho romela ho sa lekanyetsoang, litšenyehelo tse tlaase ka kakaretso.

Ka tlase, re bonts'a mohato ka mohato mokhoa oa ho iketsetsa seva sa rona sa mangolo.

## Khetho ea seva

Seva ea SMTP e ikemetseng e hloka IP ea sechaba e nang le likou tse 25, 456, le 587 tse bulehileng.

Maru a tloaelehileng a sebelisoang ke sechaba a thibetse likou tsena ka ho sa feleng, 'me ho ka khoneha ho li bula ka ho fana ka taelo ea mosebetsi, empa ho thata haholo ka mor'a tsohle.

Ke khothaletsa ho reka ho tsoa ho moamoheli ea nang le likou tsena tse bulehileng mme o ts'ehetsa ho theha mabitso a marang-rang.

Mona, ke khothaletsa [Contabo](https://contabo.com) .

Contabo ke mofani oa baeti ea lulang Munich, Jeremane, e thehiloeng ka 2003 ka litheko tsa tlholisano haholo.

Haeba u khetha Euro e le chelete ea ho reka, theko e tla ba theko e tlaase (seva e nang le memori ea 8GB le 4 CPUs e bitsa chelete e ka bang 529 yuan ka selemo, 'me tefiso ea pele ea ho kenya ke mahala bakeng sa selemo se le seng).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/UoAQkwY.webp)

Ha o etsa odara, remark `prefer AMD` , 'me seva e nang le AMD CPU e tla ba le ts'ebetso e ntle.

Ho tse latelang, ke tla nka VPS ea Contabo e le mohlala ho bonts'a mokhoa oa ho iketsetsa seva ea hau ea mangolo.

## Sebopeho sa sistimi ea Ubuntu

Sistimi ea ts'ebetso mona ke Ubuntu 22.04

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/smpIu1F.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/m7Mwjwr.webp)

Haeba seva ho ssh e bonts'a `Welcome to TinyCore 13!` (joalokaha ho bontšitsoe setšoantšong se ka tlase), ho bolela hore tsamaiso ha e e-s'o kenngoe. Ka kopo, khaola ssh 'me u eme metsotso e seng mekae ho kena hape.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/-qKACz9.webp)

Ha `Welcome to Ubuntu 22.04.1 LTS` e hlaha, qalo e felile, 'me u ka tsoela pele ka mehato e latelang.

### [Ka boikhethelo] Qala tikoloho ea ntlafatso

Mohato ona ke oa boikhethelo.

Bakeng sa boiketlo, ke kenya ts'ebetso le tlhophiso ea sistimi ea ubuntu ho [github.com/wactax/ops.os/tree/main/ubuntu](https://github.com/wactax/ops.os/tree/main/ubuntu) .

Matha taelo e latelang ho kenya ka tobetsa e le 'ngoe.

```
bash <(curl -s https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

Basebelisi ba Machaena, ka kopo sebelisa taelo e latelang, 'me puo, sebaka sa nako, joalo-joalo li tla hlophisoa ka bo eona.

```
CN=1 bash <(curl -s https://ghproxy.com/https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

### Contabo e thusa IPV6

Numella IPV6 hore SMTP e tsebe ho romela mangolo-tsoibila a nang le liaterese tsa IPV6.

fetola `/etc/sysctl.conf`

Fetola kapa eketsa mela e latelang

```
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.disable_ipv6 = 0
net.ipv6.conf.lo.disable_ipv6 = 0
```

Latela [thuto ea contabo: Ho eketsa khokahano ea IPv6 ho seva sa hau](https://contabo.com/blog/adding-ipv6-connectivity-to-your-server/)

Fetola `/etc/netplan/01-netcfg.yaml` , eketsa mela e seng mekae joalokaha ho bontšitsoe setšoantšong se ka tlase (Contabo VPS file configuration file e se e ntse e e-na le mela ena, feela u e tlose).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/5MEi41I.webp)

Ebe `netplan apply` ho etsa hore tlhophiso e fetotsoeng e sebetse.

Kamora hore tlhophiso e atlehe, o ka sebelisa `curl 6.ipw.cn` ho sheba aterese ea ipv6 ea marang-rang a hau a kantle.

## Koala li-ops tsa polokelo ea tlhophiso

```
git clone https://github.com/wactax/ops.soft.git
```

## Hlahisa setifikeiti sa mahala sa SSL bakeng sa lebitso la hau la domain

Ho romella lengolo-tsoibila ho hloka setifikeiti sa SSL bakeng sa encryption le ho saena.

Re sebelisa [acme.sh](https://github.com/acmesh-official/acme.sh) ho hlahisa setifikeiti.

acme.sh ke sesebelisoa se bulehileng sa ho saena setifikeiti,

Kenya sebaka sa polokelo ea litlhophiso ops.soft, matha `./ssl.sh` , 'me ho tla etsoa foldara ea `conf` **bukeng e ka holimo** .

Fumana mofani oa hau oa DNS ho tsoa ho [acme.sh dnsapi](https://github.com/acmesh-official/acme.sh/wiki/dnsapi) , hlophisa `conf/conf.sh` .

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Qjq1C1i.webp)

Ebe o matha `./ssl.sh 123.com` ho hlahisa `123.com` le `*.123.com` setifikeiti bakeng sa lebitso la hau la domain.

Lebelo la pele le tla kenya [acme.sh](https://github.com/acmesh-official/acme.sh) ka bo eona ebe le eketsa mosebetsi o reriloeng bakeng sa ho inchafatsa ka boiketsetso. U ka bona `crontab -l` , ho na le mola o joalo ka tsela e latelang.

```
52 0 * * * "/mnt/www/.acme.sh"/acme.sh --cron --home "/mnt/www/.acme.sh" > /dev/null
```

Tsela ea setifikeiti se hlahisitsoeng ke ntho e kang `/mnt/www/.acme.sh/123.com_ecc。`

Ntlafatso ea setifikeiti e tla letsetsa sengoloa sa `conf/reload/123.com.sh` , hlophisa mongolo ona, o ka eketsa litaelo tse joalo ka `nginx -s reload` ho nchafatsa cache ea setifikeiti sa lits'ebetso tse amanang.

## Theha seva sa SMTP ka chasquid

[chasquid](https://github.com/albertito/chasquid) ke mohloli o bulehileng oa seva ea SMTP e ngotsoeng ka puo ea Go.

E le sebaka sa li-server tsa khale tsa poso tse kang Postfix le Sendmail, chasquid e bonolo ebile e bonolo ho e sebelisa, hape e bonolo bakeng sa nts'etsopele ea bobeli.

Matha `./chasquid/init.sh 123.com` e tla kengoa ka bo eona ka ho tobetsa hanngoe feela (feta sebaka sa 123.com ka lebitso la hau la ho romella).

## Hlophisa Tshaeno ea Imeile DKIM

DKIM e sebelisoa ho romella li-signature tsa lengolo-tsoibila ho thibela mangolo ho nkuoa joalo ka spam.

Kamora hore taelo e sebetse ka katleho, o tla khothalletsoa ho seta rekoto ea DKIM (joalo ka ha ho bonts'itsoe ka tlase).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/LJWGsmI.webp)

Kenya feela rekoto ea TXT ho DNS ea hau (joalo ka ha ho bonts'itsoe ka tlase).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/0szKWqV.webp)

## Sheba boemo ba litšebeletso le litlaleho

 `systemctl status chasquid` Sheba boemo ba tshebeletso.

Boemo ba ts'ebetso e tloaelehileng bo bontšitsoe setšoantšong se ka tlase

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/CAwyY4E.webp)

 `grep chasquid /var/log/syslog` kapa `journalctl -xeu chasquid` e ka sheba tlaleho ea liphoso.

## Phetoho ea morao-rao ea lebitso la domain

Reverse domain name ke ho lumella aterese ea IP hore e rarolloe ho lebitso la domain name.

Ho beha lebitso la domain e ka morao ho ka thibela li-imeile ho tsejoa e le spam.

Ha lengolo le amoheloa, seva se amohelang se tla etsa tlhahlobo ea lebitso la domain reverse atereseng ea IP ea seva se romellang ho netefatsa hore na seva se romellang se na le lebitso la domain reverse le nepahetseng.

Haeba seva se romellang se se na lebitso la domain reverse kapa haeba domain name e ka morao e sa lumellane le aterese ea IP ea seva e romelloang, seva e amohelang e ka lemoha lengolo-tsoibila e le spam kapa ea e hana.

Etela [https://my.contabo.com/rdns](https://my.contabo.com/rdns) 'me u hlophise joalokaha ho bontšitsoe ka tlase

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/IIPdBk_.webp)

Kamora ho beha lebitso la domain reverse, hopola ho lokisa qeto ea pele ea domain name ipv4 le ipv6 ho seva.

## Fetola lebitso la moamoheli oa chasquid.conf

Fetosa `conf/chasquid/chasquid.conf` ho boleng ba domain name e furallang.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/6Fw4SQi.webp)

Ebe o matha `systemctl restart chasquid` ho qala ts'ebeletso hape.

## Boloka conf ho polokelo ea git

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Fier9uv.webp)

Mohlala, ke boloka foldara ea conf ts'ebetsong ea ka ea github ka tsela e latelang

Theha ntlo ea polokelo ea poraefete pele

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ZSCT1t1.webp)

Kenya lenane la conf 'me u le ise sebakeng sa polokelo

```
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin git@github.com:wac-tax-key/conf.git
git push -u origin main
```

## Kenya mothomeli

matha

```
chasquid-util user-add i@wac.tax
```

E ka eketsa mothomeli

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/khHjLof.webp)

### Netefatsa hore phasewete e setiloe hantle

```
chasquid-util authenticate i@wac.tax --password=xxxxxxx
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/e92JHXq.webp)

Kamora ho eketsa mosebelisi, `chasquid/domains/wac.tax/users` e tla nchafatsoa, ​​hopola ho e romella ntlong ea polokelo.

## DNS eketsa rekoto ea SPF

SPF (Sender Policy Framework) ke theknoloji ea netefatso ea lengolo-tsoibila e sebelisetsoang ho thibela bomenemene ba lengolo-tsoibila.

E netefatsa boitsebiso ba motho ea romelang mangolo ka ho hlahloba hore na aterese ea IP ea motho ea romelang e lumellana le lirekoto tsa DNS tsa domain name eo a ipolelang hore ke eona, ho thibela maqheka ho romela mangolo-tsoibila a bohata.

Ho kenya lirekoto tsa SPF ho ka thibela li-imeile ho tsejoa e le spam ka hohle kamoo ho ka khonehang.

Haeba seva sa hau sa domain name se sa tšehetse mofuta oa SPF, eketsa feela rekoto ea mofuta oa TXT.

Mohlala, SPF ea `wac.tax` e tjena

`v=spf1 a mx include:_spf.wac.tax include:_spf.google.com ~all`

SPF bakeng sa `_spf.wac.tax`

`v=spf1 a:smtp.wac.tax ~all`

Hlokomela hore ke `include:_spf.google.com` mona, sena ke hobane ke tla lokisa `i@wac.tax` e le aterese ea ho romela lebokoseng la poso la Google hamorao.

## Phetoho ea DNS DMARC

DMARC ke khutsufatso ea (Domain-based Message Authentication, Reporting & Conformance).

E sebelisoa ho tšoara li-bounces tsa SPF (mohlomong li bakoa ke liphoso tsa tlhophiso, kapa motho e mong o iketsa eka ke uena ea romellang spam).

Kenya rekoto ea TXT `_dmarc` ,

Likahare ke tse latelang

```
v=DMARC1; p=quarantine; fo=1; ruf=mailto:ruf@wac.tax; rua=mailto:rua@wac.tax
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/k44P7O3.webp)

Moelelo oa parameter ka 'ngoe o tjena

### p (Leano)

E bontša mokhoa oa ho sebetsana le mangolo-tsoibila a hlolehileng ho netefatsoa ke SPF (Sender Policy Framework) kapa DKIM (DomainKeys Identified Mail). P parameter e ka hlophisoa ho e 'ngoe ea litekanyetso tse tharo:

* ha ho letho: Ha ho na khato e nkuoang, ke sephetho sa netefatso feela se khutlisetsoang ho motho ea rometseng ka mochini oa tlaleho ea lengolo-tsoibila.
* Karantine: Kenya lengolo-tsoibila le so fetisitseng netefatso foldareng ea spam, empa le ke ke la hana lengolo ka kotloloho.
* hana: Hana ka ho toba mangolo-tsoibila a sa netefatseng.

### fo (Dikgetho tse hlolehileng)

E totobatsa palo ea lintlha tse khutlisitsoeng ke mokhoa oa ho tlaleha. E ka hlophisoa ho e 'ngoe ea litekanyetso tse latelang:

* 0: Tlaleha liphetho tsa netefatso bakeng sa melaetsa eohle
* 1: Tlaleha feela melaetsa e hlolehileng ho netefatsoa
* d: Tlaleha feela liphoso tsa netefatso ea lebitso la domain
* s: tlaleha feela liphoso tsa netefatso ea SPF
* l: Tlaleha feela liphoso tsa netefatso ea DKIM

### rua & ruf

* rua (Ho tlaleha URI bakeng sa litlaleho tse Aggregate): Aterese ea lengolo-tsoibila bakeng sa ho fumana litlaleho tse kopaneng
* ruf (Ho tlaleha URI bakeng sa litlaleho tsa Forensic): aterese ea lengolo-tsoibila ho fumana litlaleho tse qaqileng

## Kenya lirekoto tsa MX ho fetisetsa mangolo-tsoibila ho Google Mail

Hobane ha kea ka ka fumana lebokose la poso la mahala le tšehetsang liaterese tsa bokahohleng (Catch-All, e ka amohela mangolo-tsoibila leha e le afe a rometsoeng sebakeng sena sa marang-rang, ntle le lithibelo ho li-prefixes), ke sebelisitse chasquid ho fetisetsa mangolo-tsoibila kaofela ho lebokose la ka la poso la Gmail.

**Haeba u na le lebokose la poso la khoebo le lefelloang, ka kopo u se ke oa fetola MX 'me u tlōle mohato ona.**

Fetola `conf/chasquid/domains/wac.tax/aliases` , seta lebokose la mangolo la ho fetisa

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/OBDl2gw.webp)

`*` e bonts'a mangolo-tsoibila kaofela, `i` sehlomathiso sa aterese ea lengolo-tsoibila sa mosebelisi ea romelloang ka holimo. Ho fetisa mangolo, mosebelisi e mong le e mong o hloka ho kenya mohala.

Ebe u eketsa rekoto ea MX (ke supa ka kotloloho atereseng ea lebitso la domain reverse mona, joalo ka ha ho bonts'itsoe moleng oa pele setšoantšong se ka tlase).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/7__KrU8.webp)

Kamora hore litlhophiso li phetheloe, u ka sebelisa liaterese tse ling tsa lengolo-tsoibila ho romella mangolo-tsoibila ho `i@wac.tax` le `any123@wac.tax` ho bona hore na u ka fumana mangolo-tsoibila ho Gmail.

Haeba ho se joalo, sheba lethathamo la chasquid ( `grep chasquid /var/log/syslog` ).

## Romela lengolo-tsoibila ho i@wac.tax ka Google Mail

Kamora hore Google Mail e fumane lengolo leo, ke ne ke tšepile ho araba ka `i@wac.tax` ho fapana le i.wac.tax@gmail.com.

Etela [https://mail.google.com/mail/u/1/#settings/accounts](https://mail.google.com/mail/u/1/#settings/accounts) ebe o tobetsa "Kenya aterese e 'ngoe ea lengolo-tsoibila".

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/PAvyE3C.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/_OgLsPT.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/XIUf6Dc.webp)

Ebe, kenya khoutu ea netefatso e fumanoeng ke lengolo-tsoibila le rometsoeng ho eona.

Qetellong, e ka hlophisoa e le aterese ea kamehla ea motho ea romelang (hammoho le khetho ea ho araba ka aterese e tšoanang).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/a95dO60.webp)

Ka tsela ena, re phethile ho theha setsi sa mangolo a SMTP mme ka nako e ts'oanang re sebelisa Google Mail ho romella le ho amohela mangolo-tsoibila.

## Romela lengolo-tsoibila la tlhahlobo ho bona hore na tlhophiso e atlehile

Kenya `ops/chasquid`

Matha `direnv allow` ho kenya litšepiso (direnv e kentsoe ts'ebetsong ea ho qala ea senotlolo se le seng mme hoke e kentsoe khetla)

ebe matha

```
user=i@wac.tax pass=xxxx to=iuser.link@gmail.com ./sendmail.coffee
```

Moelelo oa liparamente o tjena

* mosebelisi: lebitso la mosebelisi la SMTP
* fetisa: SMTP password
* ho: moamohedi

U ka romella lengolo-tsoibila la tlhahlobo.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ae1iWyM.webp)

Ho khothaletsoa ho sebelisa Gmail ho fumana mangolo-tsoibila a tlhahlobo ho bona hore na litlhophiso li atlehile.

### TLS encryption e tloaelehileng

Joalokaha ho bontšitsoe setšoantšong se ka tlase, ho na le senotlolo sena se senyenyane, se bolelang hore setifikeiti sa SSL se atlehile ho sebetsa.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/SrdbAwh.webp)

Ebe o tobetsa "Show Original Email"

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/qQQsdxg.webp)

### DKIM

Joalokaha ho bontšitsoe setšoantšong se ka tlase, leqephe la lengolo-tsoibila la Gmail le bonts'a DKIM, ho bolelang hore tlhophiso ea DKIM e atlehile.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/an6aXK6.webp)

Sheba E amohetsoe hloohong ea lengolo-tsoibila la mantlha, 'me u ka bona hore aterese ea motho ea e rometseng ke IPV6, ho bolelang hore IPV6 le eona e lokiselitsoe ka katleho.
