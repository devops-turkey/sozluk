# DevOps ve Mikroservis Sözlüğü
### "Temellerin sağlam olmasının ilk şartı terminolojiyi iyi bilmekten geçer" - Anonim
Yazılım dünyasının "Endüstri3.0" ı olarak anlandırabileceğimiz DevOps hareketi ve ilk somut ürünlerinden olan Mikroservis yaklaşımı, beraberinde birçok alışkanlığımızın değişmesini ve doğal olarak da yeni terminolojilerin ortaya çıkmasına neden oldu.
## DevOps
Yazılımcılar(Dev) ve Operasyoncular(Ops) arasındaki işbirliğini arttırmak amacıyla ortaya çıkan bir akım.
## Artifact
Binary veya Bytecode olarak derlenmiş, çalışmaya hazır yazılım paketi. Derleme süreci gerekmeyen dillerde ise, tüm kodların toplandığı bir paket.
## Deploy
Artifact'ın bir sunucu üzerine yüklenerek, servis veriyor hale getirilmesi.
## Release
Deploy edilmiş artifact'ın canlı ortamda nihai tüketici olan gerçek müşteri veya dış/yan consumer lar tarafından tüketilmeye başlatılması
## Continuous Integration
Geliştirilen kodluk yüksek sıklıkla, tercihen günlük, tüm takım içerisinde entegre edilmesi. Entegre etmek ile beklenen unit test lerden geçmesi ve hataların düzeltilmesidir.   
## Continuous Delivery
Continuous Integration fazının çıktısı olan artifact ın gerçek bir canlı ortam adayı olup olmadığının anlaşıldığı süreçtir. Bunu anlamak adına, tercihen canlı ortamına eş, bir sunucu ortamına artifact ın deploy edilmesi ve akabinde, tercihen otomatik, fonksiyonel(UI&API)-Performans-Güvenlik testleri uygulanır. Testlerden geçerek canlı adayı olan artifact akabinde manuel olarak canlı ortama yüklenmesi işlemi başlatılır. 
## Continuous Deployment
Continuous Delivery den tek farkı, canlı ortama deploy işleminin manuel değil otomatik yapılmasıdır.
Deployment Pipeline: Continuous Integration ve Continuous Delivery fazındaki build ve kalite kontrol işlerinin yönetildiği üretim zinciri bandıdır. 
## Release Train 
Birçok ürün ve her ürünün farklı Release lerinin olduğu ortamlarda, farklı özelliklerin farklı ortamlar için kullanılmasını ve deneyimlenmesini sağlamak amaçlı periyodik olarak yapılan deploy lardır.
## Canary Deployment
Eski zamanlarda madenlerde kanaryaların oksiyen seviyesini ölçmede kullanıldığı zamanlardakine benzer, yeni bir değişikliğe karşı pazarın tepkisini ölçmek adına değişikliğin sadece küçük bir kitleye açılıp, geri dönüşe göre değişikliği gören kitleyi kademeli olarak arttırmak.  
## Blue-Green Deployment
İdealde Database dahil(Genelde dahil edilmez), tüm canlı altyapısının eş yapısına sahip "Blue" ve "Green" olarak adlandırılan iki farklı altyapı arasında deployların sırayla yapılması şeklinde trafiğin "Blue" ve "Green" arasında yer değiştirmesidir. 
## Rolling Deployment
Artifact'ın Deploy yapılacak sunucular arasında sırayla yapılmasıdır. Her yapılacak Deploy öncesi ilgili sunucudan trafik kesilir ve üzerinden aktif trafiğin bitmesi ile deploy yapılır ve akabinde trafik verilir,  bu şekilde tüm sunuculara sırayla yeni artifact yüklenmiş olur.
## Immutable Deployment
Mevcut çalışan yapıya dokunmadan, aynı yapının otomatik olarak aynısından ayağa kaldırmak suretiyle, artifact ın yeni ayağa kaldırılan sunuculara yüklenmesi ve trafiğin aktarılmasıdır. Blue - Green den fark olarak Deploy yapıldıktan sonra eski ortam ortadan kaldırılır.

## Rollback
Yazılımın bir önceki State ine geri dönülmesidir. Bu bazen bir önceki artifact versiyonuna dönmek şeklinde olabileceği gibi, bir konfigurasyon değişikliğinin geri alınması veya dış bir bağımlılık ile ilgili yapılan değişikliğin geri alınması şeklinde de olabilir. 
## Roll-forward
Rollback yaparak, yeni özellikleri canlı ortamdan geri çekmek yerine, yaşanan beklenmedik durumu düzeltme işlemidir.

## Pets vs Cattles
Pets yani evcil hayvanlar doğası gereği ilgi ister, isimleri vardır, hastalanınca bakım ister ve bu yönleriyle klasik sunucu yönetim yaklaşımı ile benzerlikleri vardır. Cattles yani sığırların ise tek tek isimleri yoktur, sayıları vardır, hastalanınca yenisi ile değiştirilir ve bu yaklaşımın yeni nesil altyapı yönetim ile benzerlikleri vardır.   
## Configuration Management
Çalışmakta olan bir İşletim Sisteminin, artifact deploy edilmeden önce üzerinde kurulması gereken bağımlılıkların ve gerekli konfigurasyonların, Declarative şekilde, tercihen Ansible, Chef veya Puppet gibi bir DSL(Domain Specific Language) kullanılarak otomatik olarak yapılmasıdır.  
## Automated Provisioning
Bir host un otomatik olarak ayağa kaldırılması ve üzerinden gerekli tüm kurulumların yapılması işlemidir.
## Infrastructure-as-code
Altyapının(Network, Switch, Firewall, AWS/GCP/Azure Cloud Resources, Host özellikleri(CPU, RAM, Disk, ...) bir DSL ile kod olarak tutulması ve tercihen versiyonlanması işlemidir.

## Auto Scaling
Belirlenen bir metriğe(CPU, RAM, Network Trafiği...) göre altyapının yatay veya dikey olarak otomatik olarak kendi kendine büyümesi işlemidir.

# Microservices
## Service Discovery
Bir bilgisayar ağındaki aygıtların ve bu aygıtlarda çalışan servislerin otomatik olarak saptanması.
## Service Registry
Servislerin ağdaki adreslerini ve ilgili bilgileri tutan veri tabanı. Genellikle yüksek erişimli, dağıtık ve tutarlı bir mimariye sahiptirler.
## CQRS(Command Query Responsibility Segregation)
Veriyi değiştiren ve veriyi sorgulayan operasyonların sorumluluklarının ayrıştırılmasını esas alan bir yazılım geliştirme modellemesi. "Okuma" ve "Yazma" için ayrı arayüzler geliştirilerek uygulanır. Performans, ölçeklenebirlik ve güvenliği maksimize eder ve sistemin geliştirilmesinde esneklik sağlar.
## Event Sourcing
Mikroservis mimarilerinde dağıtık veriyi yönetme zorluklarını çözmek için kullanılır. Verinin sadece son halini tutmak yerine, veriyi değiştimeye yönelik tüm aksiyonlar kaydedilir. Bir objenin herhangi bir andaki durumu, geçmiş aksiyonların yeniden hesaplanması ile bilinebilir.
