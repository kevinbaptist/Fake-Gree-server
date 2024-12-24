
# without docker
cd fakegree
python3 -m venv venv
source venv/bin/activate
pip install -r ../requirements.txt

openssl genpkey -algorithm RSA -out server.key
openssl req -new -key server.key -out server.csr -config openssl.cnf
openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt

python gree_server.py 192.168.1.99 1813 eu.dis.gree.com True

sudo rm /etc/systemd/system/gree_server.service  && sudo nano /etc/systemd/system/gree_server.service
sudo systemctl daemon-reload && \
    sudo systemctl enable gree_server.service && \
    sudo systemctl restart gree_server.service
sudo systemctl status gree_server.service
sudo systemctl start gree_server.service
sudo systemctl stop gree_server.service


//
sudo systemctl daemon-reload
sudo systemctl restart gree_server.service

sudo journalctl -f -u gree_server

sudo lsof -i -P -n | grep LISTEN
sudo netstat -tulpn | grep LISTEN
