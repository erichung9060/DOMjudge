# DOMjudge-docker-compose

DOMjudge 安裝流程，踩太多坑...

## 安裝流程

修改 ``` /etc/default/grub ```
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet cgroup_enable=memory swapaccount=1 systemd.unified_cgroup_hierarchy=0"
```
然後更新
```
sudo update-grub
```
記得重開機
```
sudo reboot
```

然後執行我的 docker-compose.yml

```
sudo docker-compose up -d
```

帳號是 admin
密碼要打
```
sudo docker exec -it domserver_container_name cat /opt/domjudge/domserver/etc/initial_admin_password.secret
```
container name can use ```sudo docker ps``` to check

hece, 

if the output is ```[unknown]``` ... just like me

then type

```
sudo docker exec -it domserver_container_name /opt/domjudge/domserver/webapp/bin/console domjudge:reset-user-password admin
```

then login the dashboard, click user
change "judgeaemons" password to ```9NQLNMcLCr8zu0gB```

![image](https://user-images.githubusercontent.com/50062014/199960685-2db1e22b-6e95-4afb-88e0-7e668f1c15e8.png)

如果 Judgehosts 有多的　Judgehosts　那就是成功了，不然用　docker container logs 也可以看出來

這邊可能有幾個問題
1. grub 設定沒設
2. 401 驗證過不去
3. url 打不到 server

這照著我上面弄就可以解決了

![image](https://user-images.githubusercontent.com/50062014/199961181-061f0dd3-b430-49fe-b1e9-22c668091110.png)


## Note
