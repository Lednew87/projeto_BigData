# projeto_BigData
Repositório para a conclusão de desafio de projeto Explorando Dados Demográficos com Serviços de Big Data na AWS.

Instruções para atividade prática sob orientação do expertDIO Cassiano Peres.

Kinesis Delivery Stream
AWS Console -> Kinesis -> Create Firehose Delivery Stream "StreamName" -> Direct PUT -> Next -> Choose Destination -> Create S3 Bucket “covid-vaccines-logs-diolive” -> Configure settings -> buffer size 5mb -> buffer interval 60s -> IAM Role -> create new role -> Review and create

EC2
AWS Console -> EC2 -> Amazon Linux 2 AMI -> t2micro -> review and launch -> create new key pair -> download .pem file -> download putty -> puttygen -> load.pem file -> save .ppk file -> putty copy dns -> paste hostname -> SSH -> auth -> load ppk file -> login “ec2-user”

sudo yum install -y aws-kinesis-agent
sudo yum install -y git
git clone https://github.com/cassianobrexbit/dio-live-aws-bigdata-2.git
unzip Dataset.zip
chmod a+x LogGenerator.py
nano LogGenerator.py
less country_vaccinations.csv
sudo mkdir /var/log/diolive
cd /etc/aws-kinesis
sudo nano agent.json
Copiar conteúdo do arquivo agent.json
agent.json -> "kinesis.endpoint": "kinesis..amazonaws.com"
AWS Console -> EC2 -> Instances -> Select Instance -> Security -> Modify IAM Role -> Create New Role -> EC2 -> Administrator Access -> rolename “ec2-admin-role” -> save

sudo service aws-kinesis-agent start
sudo chkconfig aws-kinesis-agent on (start with instance)
_cd ~_
sudo ./LogGenerator.py 500000
tail -f /var/log/aws-kinesis-agent/aws-kinesis-agent.log

S3
AWS Console -> S3 -> select bucket -> selecionar arquivo e download

SSH EC2
sudo service aws-kinesis-agent restart
sudo ./LogGenerator.py
tail -f /var/log/aws-kinesis-agent/aws-kinesis-agent.log
AWS Console -> Kinesis Streams -> select stream -> monitoring

AWS Glue
AWS Console -> glue databrew -> create new project -> create new role -> create project
Create dataset -> S3 -> formato CSV
