[toc]
### 服务器clash配置

#### clash 下载
在 Clash [release](https://github.com/Dreamacro/clash/releases) 页面下载相应的版本，对于 Ubuntu 一般使用 clash-linux-amd64-vX.X.X.gz 版本：

```
wget https://github.com/Dreamacro/clash/releases/download/v1.10.0/clash-linux-amd64-v1.10.0.gz
```

然后使用 gunzip 命令解压，并重命名为 clash：
```
gunzip clash-linux-amd64-v1.10.0.gz
mv clash-linux-amd64-v1.10.0 clash
```

为 clash 添加可执行权限：
```
chmod u+x clash
```

Clash 运行时需要 Country.mmdb 文件，当第一次启动 Clash 时（使用 ./clash 命令） 会自动下载（会下载至 /home/XXX/.config/clash 文件夹下）
- Country.mmdb 文件利用 GeoIP2 服务能识别互联网用户的地点位置，以供规则分流时使用。

若是下载失败， 也可使用[此链接](https://github.com/Dreamacro/maxmind-geoip/releases)

#### 配置文件
clash运行需要`clash.yaml`文件, 一般机场会提供订阅文件或者链接, clash for windows中有个`show in folder`的选项, 可以找到`.yml`文件, 重命名为`config.yaml`即可.
![image](https://img2022.cnblogs.com/blog/2050897/202207/2050897-20220707131632591-1969461732.png#pic_center)

然后把`config.yaml`复制到`/home/XXX/.config/clash 文件夹下`

#### 使用代理
Clash 运行后，其在后台监听某一端口。Ubuntu 下使用代理，需要 export 命令。根据 config 配置文可以查看到件Clash 代理端口
```
export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890
```


取消系统代理：
```
unset  http_proxy  https_proxy
```

- 还有说设置**all_proxy**的, 我没有设置这个就可以用了
```
export all_proxy=socks5://127.0.0.1:7890

unset all_proxy
```

### 图形界面
- 不需要命令了，只用系统改
![image](https://img2022.cnblogs.com/blog/2050897/202208/2050897-20220822164229245-1301787324.png)


### youtube-dl命令

youtube-dl默认不使用代理, 可以加入`--proxy ip:端口` 的命令
```
youtube-dl --proxy "127.0.0.1:7890"
```

### git 命令
```
git clone https://github.com/sicxu/Deep3DFaceRecon_pytorch.git --config "http.proxy=127.0.0.1:7890"
```
git config --global https.proxy http://127.0.0.1:1080

git config --global https.proxy https://127.0.0.1:1080

git config --global --unset http.proxy

git config --global --unset https.proxy



### apt-get 命令
```
sudo apt-get -o Acquire::http::proxy="http://127.0.0.1:7890/" update
sudo apt-get install -o Acquire::http::proxy="http://127.0.0.1:7890/"  libc6-dev-i386
```
