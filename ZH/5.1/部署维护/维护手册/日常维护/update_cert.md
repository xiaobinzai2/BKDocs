# 更新证书

有时候 GSE 和 License 所在服务器的 MAC 地址发生了变化，此时证书需要重新从官网生成下载，然后操作更新证书的步骤

中控机上解压新的证书

```bash
cd /data/src/cert && rm -f *
tar -xvf /data/ssl_certificates.tar.gz -C /data/src/cert/
```

操作更新相关组件

```bash
./bkcec update cert
./bkcec install gse 1
./bkcec stop gse
./bkcec start gse
./bkcec stop bkdata
./bkcec start bkdata
./bkcec stop fta
./bkcec start fta
```

Proxy 和 Agent 的更新，需要把新的 cert 目录传到对应机器的路径：

- agent: `/usr/local/gse/agent/cert/`
- windows: `C:\gse\agent\cert\`
- proxy: `/usr/local/gse/proxy/cert/`

然后重启进程：

- 重启 agent: `/usr/local/gse/agent/bin/gsectl restart`
- 重启 windows_agent：`C:\gse\agent\bin>gsectl.bat restart`
- 重启 proxy: `/usr/local/gse/proxy/bin/gsectl restart`
