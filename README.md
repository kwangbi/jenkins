-- jenkins 설치
sudo yum update -y

sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo

sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key

sudo yum install jenkins -y

sudo service jenkins start

-- jdk8
sudo yum install -y java-1.8.0-openjdk-devel.x86_64
sudo /usr/sbin/alternatives --config java


-- maven 설치
sudo wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo
sudo sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo
sudo yum install -y apache-maven
mvn --version

--nginx 설치
sudo yum install nginx -y
sudo amazon-linux-extras install nginx1
sudo vim /etc/nginx/nginx.conf

location / {
		proxy_pass http://localhost:8080;
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_set_header Host $http_host;
}

sudo service nginx start


-- git 설정
git config --global user.name "kwangbi"
git config --global user.email "kwangbi@naver.com"

git init

git config --global --list
git status



echo "# jenkins" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/kwangbi/jenkins.git
git push -u origin main