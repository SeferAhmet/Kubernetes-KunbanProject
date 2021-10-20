Proje mimarisinde goruldugu uzere, 3 katmandan olusmaktadir.
-----------------------------------------------------------------------------------
Ilk katman olan database katmaninda, database engine olarak postgres kullanilacaktir.
Postgres, 1 replicadan olusan deployment olarak deploy edilecektir.
Image olarak postgres:9.6-alpine kullanilacaktir.
Verilerin kalici olmasi icin bir Persisten volume e ihtiyac vardir.Bu yuzden deployment ta bir PVC tanimlanacak,
postgres container inion /var/lib/postgresql/data klasorune mount edilecektir.
postgres imajinin konfigiurasyonu icin, POSTGRES_DB, POSTGRES_USER ve POSTGRES_PASSWORD env leri belirlenecek ve CM veya secret olarak
container a eklenecektir.
Postgres in default port u expose edilecektir.
-------------------------------------------------------------------------------
Backend olarak kanban-app yazilimi kullanilacaktir.
Image :3808544/kanban-board_kanban-app
Kanban-app port u 8080 olacaktir.
Kanban-app in db ye baglanmasi icin gerekli parametreler env olarak deployment a dahil edilecektir.
---------------------------------------------------------------------------------
Frontend olarak nginx kullanilacaktir. Gerekli yonlendirme islemleri halihazirda tanimlanmis olan
3808544/kanban-board_kanban-ui imaji kullanilacaktir.
---------------------------------------------------------------------------------
Proje mimarisinde gorulecegi uzere database uzerindeki verileri gormeyi saglayacak olan
adminer yazilimi icin bir deployment hazirlanacak ve imaj olarak adminer:4.7.6-standalone
imaji kullanilacaktir.
Uygulamanin default port u 8080 expose edilecek, env variable olarak
ADMINER_DESIGN:pepa-linha, ADMINER_DEFAULT_SERVER:postgres olacak sekilde deployment a dahil edilecektir.
----------------------------------------------------------------------------------
Tum uygulamalar birbirleri ile servisler uzerinden haberlesmesi saglanacaktir.
-----------------------------------------------------------------------------------
Disaridan uygulamaya son kullanicilarin ulasabilmesi icin ingres tanimlanacaktir.
http://kanban.k8s.com adresi web browser dan girildiginde kanban forntend e,  
http://kanban.k8s.com/api/ adresi girildiginde backend e,
http://adminer.k8s.com girildiginde adminer deployment ina ulasilmalidir.