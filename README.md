# AWS’de ECS Fargete, VPC VE RDS kullanarak MYSQL ile Word Press Alt Yapısı Projesi

### Amazon ECS: 
Amazon Elastic Container Service (Amazon ECS), bir clusterdaki containerları çalıştırmayı, durdurmayı ve yönetmeyi kolaylaştıran, oldukça ölçeklenebilir, hızlı bir container yönetim hizmetidir. Containerlarınız, taskları çalıştırmak için kullandığınız bir task definitionda tanımlanır. Tasklarınızı ve ECS Servicelerinizi AWS Fargate tarafından yönetilen sunucusuz bir altyapı üzerinde çalıştırabilirsiniz. Alternatif olarak, altyapınız üzerinde daha fazla kontrol sahibi olmak için tasklarınızı ve ECS Servicelerinizi yönettiğiniz bir Amazon EC2 bulut sunucusu çalıştırabilirsiniz.Basit bir ifadeyle Docker containerlarınızı AWS platformu üzerinde isterseniz EC2 sunucularında ya da Fargate servisini kullanarak serverless yani sunucu yönetimini tamamen AWS ‘ye bırakarak dağıtmanızı ve yönetmenizi sağlayabilirsiniz.

### CLUSTER: 
ECS Cluster, üzerinde taskları ve ECS Service’leri çalıştırabilmek için bir veya daha fazla EC2 instance kapsayabilirler ya da Fargate’in sağladığı serverless yapıda task ve ECS Service’leri çalıştırmak için kullanabiliriz.

### TASK DEFINITION: 
Task definitionlar çalıştıracağınız taskların kurallarını belirler. Çalıştıracağınız task veya taskın içindeki her bir containerın ne kadar CPU ve bellek kullanacağını, environment değişkenlerini,containerların port bilgilerini, task ın hangi IAM Role sahip olacağını, imagelarınızı barındırdığınız ECR veya DockerHub gibi repoların Urllerini, private repolar ise bunların authentication bilgileri task definitionlarda saklanır.

### SERVICE: 
Bir Amazon ECS Service’i, ECS Clusterda eş zamanlı olarak task definitionda tanımlanan kurallara göre belirtilen sayıda tasklarınızı çalıştırmaya olanak tanır. Tasklardan herhangi birinin bir sebeple başarısız olması ya da durdurulması durumunda service’de istenilen sayıda task’ı sürdürmek için yeni bir task başlatır.

### RDS: 
AWS tarafından sağlanan yönetilen bir SQL veritabanı hizmetidir. Amazon RDS, verileri depolamak ve düzenlemek için bir dizi veritabanı motorunu destekler. Ayrıca veri taşıma, yedekleme, kurtarma ve yamalama gibi ilişkisel veritabanı yönetimi görevlerinde de yardımcı olur. Amazon RDS, buluttaki ilişkisel veritabanlarının dağıtımını ve bakımını kolaylaştırır. Bir bulut yöneticisi, bir bulut veritabanının ilişkisel örneğini kurmak, işletmek, yönetmek ve ölçeklendirmek için Amazon RDS'yi kullanır . Amazon RDS'nin kendisi bir veritabanı değildir; ilişkisel veritabanlarını yönetmek için kullanılan bir hizmettir.

# 

![This is an image](https://github.com/haticedikmn/AWS_ECS_VPC_RDS_ile_Word_Press_Alt_Yapisi_Kurmak/blob/main/image/1.png)<br/><br/>

</div>

1- ECS – RDS kullanarak bir wordpress altyapısı kuracağız. 

2- Mysql rds te çalışacak, application sunucusu ECS (farget) te çalışacak.

3- VPC üzerinden birbirleri ile haberleşecekler

<div align="center">

###  N. Virginia’ya girerek ilk adım olarak VPC kuruyoruz.

![This is an image](https://github.com/haticedikmn/AWS_ECS_VPC_RDS_ile_Word_Press_Alt_Yapisi_Kurmak/blob/main/image/2.png)<br/><br/>

</div>

Create tuşuna basarak oluşturma işlemini tamamladım. Bu VPC’yi kurduğum anlamına geliyor.
 
<div align="center">

### RDS ‘te MYSQL KURMA AŞAMASI;

![This is an image](https://github.com/haticedikmn/AWS_ECS_VPC_RDS_ile_Word_Press_Alt_Yapisi_Kurmak/blob/main/image/4.png)<br/><br/>

</div>
Database kurma aşamasını ttamamlayarak ECS Servisine geçiyorum.

<div align="center">

### ECS OLUŞTURMA AŞAMASI;

</div>

Create Cluster tuşuna basarak ECS oluşturma basamağına geçiyoruz.

<div align="center">

![This is an image](https://github.com/haticedikmn/AWS_ECS_VPC_RDS_ile_Word_Press_Alt_Yapisi_Kurmak/blob/main/image/11.png)<br/><br/>
![This is an image](https://github.com/haticedikmn/AWS_ECS_VPC_RDS_ile_Word_Press_Alt_Yapisi_Kurmak/blob/main/image/15.png)<br/><br/>

</div>

ECS oluşturma işlemini tamamladım.

<div align="center">

### Task Definition Oluşturma Aşaması

![This is an image](https://github.com/haticedikmn/AWS_ECS_VPC_RDS_ile_Word_Press_Alt_Yapisi_Kurmak/blob/main/image/16.png)<br/><br/>

</div>

YENİ BİR TASK OLUŞTURMAK İÇİN IAM CONSOLA GİDİYORUZ VE AŞAMALARI;

<div align="center">

![This is an image](https://github.com/haticedikmn/AWS_ECS_VPC_RDS_ile_Word_Press_Alt_Yapisi_Kurmak/blob/main/image/18.png)<br/><br/>

</div>

Mysql’in RDS ile konuşabilmesi için Task Rolünü oluşturmamız gerekli IAM Console giderek gerekli rollleri oluşturuyoruz.
 
<div align="center">

![This is an image](https://github.com/haticedikmn/AWS_ECS_VPC_RDS_ile_Word_Press_Alt_Yapisi_Kurmak/blob/main/image/23.png)<br/><br/>

</div>

IAM Role oluşturma işlemimiz tamam.

<div align="center">

### AWS ECS – Clusters bölümüne gelerek servis oluşturmaya başlayalım.

![This is an image](https://github.com/haticedikmn/AWS_ECS_VPC_RDS_ile_Word_Press_Alt_Yapisi_Kurmak/blob/main/image/35.png)<br/><br/>

</div> 
 
Oluşturduğumuz servis içinde tasklara girerek IP adresi ile bağlantı işlemini gerçekleştirdim.
 
<div align="center">

![This is an image](https://github.com/haticedikmn/AWS_ECS_VPC_RDS_ile_Word_Press_Alt_Yapisi_Kurmak/blob/main/image/36.png)<br/><br/> 
 
</div>  

ECS attığımız konteynırın fargete ile çalıştığını IP adresi ile girdiğimizde anlıyoruz. WordPress verilerini de çektiğini görüyoruz.
 
<div align="center">

![This is an image](https://github.com/haticedikmn/AWS_ECS_VPC_RDS_ile_Word_Press_Alt_Yapisi_Kurmak/blob/main/image/37.png)<br/><br/> 
![This is an image](https://github.com/haticedikmn/AWS_ECS_VPC_RDS_ile_Word_Press_Alt_Yapisi_Kurmak/blob/main/image/38.png)<br/><br/> 

 
### MySQL ile veritabanına bağlanma aşaması son aşamamız.

</div>  
•	Kullandığınız herhangi bir veri tabanının host kısmına AMAZON RDS – Databases – Connectivity & Security kısmından endpoint kısmındaki adresi yazıyoruz(örnek: wordpressuygulamasi.cpemrwnikfj0.us-east-1.rds.amazonaws.com).

•	RDS oluştuturken oluşturduğunuz kullanıcı adı ve password’u  da yazarak veri tabanına bağlanabilirsiniz.

