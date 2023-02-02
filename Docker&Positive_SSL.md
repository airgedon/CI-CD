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

Enter the directory where you uploaded the certificate files. Run the following command to combine the files:

```
cat your_domain.crt your_domain.ca-bundle >> your_domain_chain.crt
```

Please note that if the certificate files were downloaded from your Namecheap account, the best command to use will be:

```
cat your_domain.crt > your_domain_chain.crt ; echo >> your_domain_chain.crt ; cat your_domain.ca-bundle >> your_domain_chain.crt

```
> ssh into your server

sudo mkdir /etc/nginx/ssl

sudo nano /etc/nginx/ssl/bundle.cer and copy the bundle.cer file’s contents from your development machine and paste it into this file. Save & exit (Ctrl+X; Yes).

sudo nano /etc/nginx/ssl/key.pem and copy the key.pem file’s contents from your development machine and paste it into this file. Save & exit.

Protect that directory: sudo chmod 600 /etc/nginx/ssl























[Source](https://bradddd.com/setting-up-namecheap-comodo-positivessl-certificate-in-nginx-with-docker/)
