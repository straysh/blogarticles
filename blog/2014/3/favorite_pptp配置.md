{
    "id": 21,
    "user_id": 1,
    "category_id": 5,
    "author": "straysh",
    "title": "pptp配置",
    "slug": "favorite_pptp配置",
    "hits": 80,
    "published_at": "1394688326",
    "created_at": 1394688326,
    "updated_at": 1504844417,
    "deleted_at": null
}
```bash
1.yum -y install ppp pptp
2.vim /etc/ppp/chap-secrets
# Secrets for authentication using CHAP
# client    server  secret          IP addresses
vpn帐号   vpnIP vpn密码 *

3.vim /etc/ppp/peers/phpcurl
pty 'pptp vpnIP --nolaunchpppd'
name vpn帐号
remotename vpnIP
require-mppe-128
file /etc/ppp/options.pptp
ipparam phpcurl

4.vim /etc/ppp/options.pptp

lock
noauth
refuse-pap
refuse-eap
refuse-chap
nobsdcomp
nodeflate
require-mppe-128

5.pppd call phpcurl
6.route del default dev eth0
7.route add default dev ppp0
```
