# 请勿泄露源码给他人，当你让他人为你debug或进行其他操作时，切勿让他访问你网站的全部代码，尤其是不认识的人。泄露源码对你我都没好处。
# 不能删改页面底部的 Powered by SSPANEL. Theme by editXY，不能删改staff页面的任何信息。
## 安装

本主题包含了SSPANEL的完整代码，需要删除原来的面板，然后全新安装（数据库通用），操作前请备份面板

在网站目录下 
`git clone -b malio https://gitlab.com/maxitio/malio-theme-for-sspanel.git tmp && mv tmp/.git . && rm -rf tmp && git reset --hard`

根据 [sspanel的wiki](https://blog.anank.ke/w/SSPanel_with_DROP_DATABASE_BT) 安装后，将config目录下的.malio_config.example.php 复制一份命名为 .malio_config.php，可以用这个命令 `cp config/.malio_config.example.php config/.malio_config.php`

修改.config.php里的 `$System_Config['theme']` 的值为malio



客户端的安装包需要自行下载到 `/public/client-download/` 目录，安装包名字参考同目录下的 apps.txt 文件，另外在此目录下还提供了 [download.sh](https://github.com/sspanel-uim/ssr-download-updater) 脚本，可自动下载部分客户端。

部署好了之后就可以找我拿js授权文件，js授权文件需要重命名为 `malio.js` 并放入 `/public/theme/malio/js/` 文件夹内。每次更新js授权文件后，需要在 .malio_config.php 里更改 malio_js_version 的值，以确保用户浏览器会获取到最新的js授权文件，套了CF的话记得清除CF的缓存。

## 数据库操作
如果你的数据库以前已经进行过以下与数据库相关的操作的话，请跳过。

进行以下操作时请先备份数据库。

将数据库user表里的全部用户的theme列改为malio，可以使用这条SQL语句👉 `UPDATE user SET theme='malio'`

将 `/sql/malio_all.sql` 导入到数据库

将 `sql/user_subscribe_log.sql` 导入到数据库（用户订阅记录，没有导入的话会导致无法订阅）

将 `sql/detect_ban_log.sql` 导入到数据库（审计封禁表）

在网站目录下执行 `php xcat GenerateUUIDforAllUsers`

## 注意事项
.malio_config.php 文件里的商品id必须设置好，不然在商店plans模式下没办法购买。

在.config.php里设置新用户注册等级为-1，如果不设置为-1的话，就没有新手引导教程，同时需要在.config.php里设置用户等级过期时间，建议设置为超过一个月的时间(720小时)。

安装完成后如果旧用户无法登录的话，检查下 .config.php 里面的 salt 和 pwdMethod 的值是否跟原来的 .config.php 一致。

端口偏移的说明查看 [端口偏移的食用方法](https://678765.xyz/2019/2.html)，根据群友说支持普通端口和单端口，格式跟uim原版的偏移不一样

如果需要配置Stripe支付接口的话，请看本仓库的wiki

## Telegram
[TG群组](https://t.me/joinchat/DM2_FxStXAbYZ2DzVfZjcw)

[TG频道](https://t.me/malio_for_sspanel) ，有新功能或优化都会在频道里发广播，所以请一定要关注频道

## CREDIT
基于 [rico](https://github.com/rico93) 和 [GeekQu](https://github.com/GeekQu) 维护的 [ss-panel-v3-mod_Uim](https://github.com/rico93/ss-panel-v3-mod_Uim) 修改

## Malio.js 授权文件更新记录

