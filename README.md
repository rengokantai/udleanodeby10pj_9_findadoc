#### udleanodeby10pj_9_findadoc
######1
install cassandra(as of 04/2016 3.5)
```
echo "deb http://www.apache.org/dist/cassandra/debian 35x main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list &&
echo "deb-src http://www.apache.org/dist/cassandra/debian 35x main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list &&
gpg --keyserver pgp.mit.edu --recv-keys F758CE318D77295D &&
gpg --export --armor F758CE318D77295D | sudo apt-key add - &&
gpg --keyserver pgp.mit.edu --recv-keys 2B5C1B00 &&
gpg --export --armor 2B5C1B00 | sudo apt-key add - &&
gpg --keyserver pgp.mit.edu --recv-keys 0353B12C &&
gpg --export --armor 0353B12C | sudo apt-key add - &&
sudo apt-get update -y && sudo add-apt-repository ppa:webupd8team/java -y &&
sudo apt-get update -y&&
sudo apt-get install oracle-java8-installer && sudo apt-get install cassandra -y
```
check
```
service cassandra status
```

######2 create table
```
create keyspace findadoc with replication ={'class':'SimpleStrategy','replication_factor':3} and durable_writes=true;
describe keyspaces;
use findadoc;
create table doctors(doc_id uuid,full_name text,category text,practice_name text,street text,city text,state text,new_patients boolean,grad_year int,primary key(doc_id,full_name,category,city,state));
create index on doctors(state);
create table categories(cat_id uuid,name text, primary key(cat_id));
insert into doctors(doc_id,full_name,category,practice_name,street,city,state,new_patients,grad_year) values (now(),'Ke','Podiatrist','Ke Medical','100 Street','Wood','NY',true,2015);
insert into doctors(doc_id,full_name,category,practice_name,street,city,state,new_patients,grad_year) values (now(),'Hernan','Pediatrician','Hernan Medical','1 Street','Bay','CA',true,2014);
select * from doctors;
insert into categories(cat_id,name)values(now(),'Podiatrist');
insert into categories(cat_id,name)values(now(),'Pediatrician');
select * from categories;
```
