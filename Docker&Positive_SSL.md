> Local machine: in the folder created
```
sudo openssl genrsa 2048 > key.pem
```
```
sudo openssl dhparam -out dhparams.pem 2048
```
```
sudo openssl req -new -key key.pem -out csr.pem
```
> copy and paste the contents of the csr.pem file to the form on NameCheap when prompted to following the purchase.




























[Source](https://bradddd.com/setting-up-namecheap-comodo-positivessl-certificate-in-nginx-with-docker/)
