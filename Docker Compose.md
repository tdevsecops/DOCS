
( Alpine ‹--- Ubuntu )


Pull alpine images

	$ docker pull alpine

Run the alpine image

	$ docker run -it alpine

update alpine

	 $ apk update 

install nmap and apache2 in alpine 

	$ apk add nmap apache2 nano

Check if the packages are installed

	$ nmap -version

	$ httpd -v

Now edit the apache .conf at `/etc/apache2/httpd.conf`

	$ nano /etc/apache2/httpd.conf

in this file find and uncomment  `ServerName` and change to `localhost`

	#ServerName www.example.com:80

	ServerName localhost

Exit the container without shutting down the container by

	Ctrl+P Ctrl+Q

Pull a ubuntu image using docker

	$ docker pull ubuntu:latest

update ubuntu 

	$ apt update

Install python3 in ubuntu container

	$ apt install python3 iproute2

Create a dummy file in the current directory

	$ echo "ABCDEFGHIJKLMNOPQRSTUVWXYZ" >> potasticp.txt

also fetch the ip address of the container

	$ ip a

Note the ip address for the container

Now start a python server on port 80 `'default port :8000 if not set'` in the current directory

	$ python3 -m  http.server 80


	Ctrl+P Ctrl+Q

List the running docker container using

	$ docker ps

There will be 2 containers alpine and ubuntu

	CONTAINER_ID    NAME
	54ds6f5sdf4sd   alpine   ...
	d4a6f4a6sdf4a   ubuntu   ...

Switch to alpine container using

	$ docker attach <Container_ID>

Use nmap to scan the ubuntu container to see if the intended ports are open and running

	$ nmap <Ubuntu_ip_address> -p-

now try to download the `potasticp.txt` from ubuntu using `wget`

	$ wget http://X.X.X.X:80/potasticp.txt

check if the file is downloaded with `ls`

	$ ls

( Alpine ---› Ubuntu )

Similarly create a dummy file in alpine container at `/var/www/localhost/htdocs/<dummy>`

	$ echo "abcdefghijklmnopqrstuvwxyz" >> /var/www/localhost/htdocs/beba.txt

and note is `ip`  using 

	$ ip a

Start the apache service in foreground using

	$ httpd -DFOREGROUND 

	Ctrl+P Ctrl+Q

Switch to alpine container using

	$ docker attach <Container_ID>

And try downlaoding the `beba.txt` from alpine container

	$ wget http://X.X.X.X/beba.txt


check if the file is downloaded with `ls`

	$ ls
