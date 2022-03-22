linux 机器通过梯子访问外网

1、准备环境：
需要有clash-linux版本执行文件，需要有clash可读文件，需要做代理

2、上传clash-linux-amd64-v1.7.1 到root下

3、上传clash到/root/.config/文件夹下

4、设置代理
export http_proxy=http://127.0.0.1:7890
export https_proxy=http://127.0.0.1:7890

5、run二进制文件
./clash-linux-amd64-v1.7.1

6、docker proxy配置代理

mkdir -p /etc/systemd/system/docker.service.d 
touch /etc/systemd/system/docker.service.d/proxy.conf
chmod 777 /etc/systemd/system/docker.service.d/proxy.conf
echo '
[Service]
Environment="HTTP_PROXY=http://127.0.0.1:7890/"
Environment="HTTPS_PROXY=http://127.0.0.1:7890/"
' >> /etc/systemd/system/docker.service.d/proxy.conf
systemctl daemon-reload
systemctl restart docker