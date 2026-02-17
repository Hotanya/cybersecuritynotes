# Setup

* apt get golang
* sudo git clone https://github.com/gophish/gophish.git
* `cd gophish`
* Remove identifiers

{% code overflow="wrap" lineNumbers="true" %}
```

sudo find . -type f -exec sed -i.bak1 's/X-Gophish-Contact/X-Contact/g' {} + sudo find . -type f -exec sed -i.bak2 's/X-Gophish-Signature/X-Signature/g' {} + sudo find . -type f -exec sed -i.bak3 's/ServerName\ =\ "gophish"/ServerName\ =\ "IGNORE"/g' {} + sudo sed -i.bak4 's/const RecipientParameter = "rid"/const RecipientParameter = "x"/g' models/campaign.go
```
{% endcode %}

`sudo go build`

`nano config.json`

* change port to something different e.g 3334
* go to ec2 security groups, add in the new port you specified
* `sudo ./gophish`
* Navigate to https://$EC2PublicIP:3334



* End gophish server
* install certbot&#x20;
* sudo apt install certbot
* sudo certbot certonly -d YOURDOMAIN --register-unsafely-without-email
  * Select Option 1 (standalone)
  * Copy the certs mentioned to gophish directory

In config.json, replace phish\_server deets:

* listen url to `0.0.0.0:443`
* use\_tls to `true`
* cert path to `fullchain.pem` (created from certbot)
* key\_path to `privkey.pem` (created from certbot)

![](<../../.gitbook/assets/image (1).png>)

restart gophish server

Confirm it is running properly\
&#x20;![](<../../.gitbook/assets/image (8).png>)



