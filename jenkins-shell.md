# Job1 - slave
```
sudo apt update -y
sudo apt install git python3 openssh-server -y
```
# Job2 - master
```
sudo ansible-playbook -i ansible/playbook.yaml
```
# Job3 - slave
```
sudo docker stop $contaner_name || true
sudo docker rm $contaner_name || true
sudo docker build -t $image_name .
sudo docker run -d --name $container_name -p $container_port:80 $image_name
sudo sleep 5s
status_code=$(curl -s -o /dev/null -w "%{http_code}" 0.0.0.0:$container_port)
if ["$status_code" != 200]
then
	echo "BUILD FAILED"
    exit 1
fi
```
