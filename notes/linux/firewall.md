# 防火墙配置

## 查看防火墙状态

```
systemctl status firewalld
```

## 开启防火墙和开机自启

```
systemctl start firewalld
systemctl enable firewalld
```

## 开放或限制端口

```
firewall-cmd --zone=public --add-port=22/tcp --permanent
```
其中 `--permanent ` 为设置永久生效，不加的话机器重启之后失效


```
firewall-cmd --reload
```
重载防火墙更新配置


```
firewall-cmd --zone=public --query-port=22/tcp
```
查看是否生效

```
firewall-cmd --zone=public --list-ports
```
查看所有开发的端口


## 限制端口

```
firewall-cmd --zone=public --remove-port=22/tcp --permanent
```
限制端口

```
firewall-cmd --reload
```
重载生效


## 批量开发或限制端口

```
firewall-cmd --zone=public --add-port=100-500/tcp --permanent
```
批量开放100 - 500

```
firewall-cmd --zone=public --remove-port=100-500/tcp --permanent
```
批量限制100-500


## 限制ip访问

```
firewall-cmd --permanent --add-rich-rule="rule family="ipv4" source address="192.168.0.1" port protocol="tcp" port="80" reject"
```
限制ip访问80

```
firewall-cmd --permanent --add-rich-rule="rule family="ipv4" source address="192.168.0.1" port protocol="tcp" port="80" accept"
```
接触限制ip访问80

```
firewall-cmd --permanent --add-rich-rule="rule family="ipv4" source address="0.0.0.0/0" port protocol="tcp" port="80" reject"
```
限制ip段

```
firewall-cmd --permanent --add-rich-rule="rule family="ipv4" source address="0.0.0.0/0" port protocol="tcp" port="80" accept"
```
解除限制ip段
