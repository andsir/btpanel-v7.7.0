# btpanel-v7.7.0
btpanel-v7.7.0-backup  官方原版v7.7.0版本面板备份

**Centos/Ubuntu/Debian安装命令 独立运行环境（py3.7）**

```Bash
curl -sSO https://raw.githubusercontent.com/andsir/btpanel-v7.7.0/main/install/install_panel.sh && bash install_panel.sh
```



# 手动破解：

1，屏蔽手机号

```
sed -i "s|bind_user == 'True'|bind_user == 'XXXX'|" /www/server/panel/BTPanel/static/js/index.js
```

2，删除强制绑定手机js文件

```
rm -f /www/server/panel/data/bind.pl
```

3，手动解锁宝塔所有付费插件为永不过期

文件路径：`/www/server/panel/data/plugin.json`

搜索字符串：`"endtime": -1`全部替换为`"endtime": 999999999999`

4，给plugin.json文件上锁防止自动修复为免费版

```
chattr +i /www/server/panel/data/plugin.json
```

============================

！！如需取消屏蔽手机号

```
sed -i "s|if (bind_user == 'REMOVED') {|if (bind_user == 'True') {|g" /www/server/panel/BTPanel/static/js/index.js
```

5. 宝塔破解付费插件
注：plugin.json需登录1次面板后生成

文件路径：www/server/panel/data/plugin.json
搜索"endtime": -1 全部替换为"endtime": 999999999999
搜索 "ltd": -1, "pro": -1 替换 "ltd": -1, "pro": 0 
pro为0时为专业版永久授权

6. 禁止宝塔面板检测升级，防止失效
查找字符串：name": "coll_admin"，将这段里的update_mgs删除或者改为null

7. 禁止解锁插件后自动修复为免费版
文件路径：www/server/panel/data/repair.json
查找字符串："id": 16，将这段修复权限的代码删除

8. 限制修改
```
chattr +i /www/server/panel/data/plugin.json
chattr +i /www/server/panel/data/repair.json
```
9. 等修改完成，并且安装好付费插件后开启面板的离线模式。 不开离线模式宝塔下次打开还会自动读取云端列表，给你恢复未授权。 
