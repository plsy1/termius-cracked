# Termius-cracked

## 注意事项
1. 修改完后开启Termius会弹XXX is damaged and can’t be opened. You should move it to the Trash (Mac)  
   解决办法：关闭SIP状态下执行`xattr -rc /Applications/Termius.app`
## 步骤
1. 解包app.asar
```shell
cd /Applications/Termius.app/Contents/Resources/
asar extract app.asar ./app
mv app.asar app.asar.bak
rm app-update.yml
```
2. 修改app/js/background-process.js

搜索`const await this.api.bulkAccount`,将const改为var  

在`var e=await this.api.bulkAccount();`后添加如下代码

```js
e.account.pro_mode=true;e.account.need_to_update_subscription=false;e.account.current_period={"from":"2022-01-01T00:00:00","until":"2099-01-01T00:00:00"};e.account.plan_type="Premium";e.account.user_type="Premium";e.student=null;e.trial=null;e.account.authorized_features.show_trial_section=false;e.account.authorized_features.show_subscription_section=true;e.account.authorized_features.show_github_account_section=false;e.account.expired_screen_type=null;e.personal_subscription={"now":new Date().toISOString().slice(0,-5),"status":"SUCCESS","platform":"stripe","current_period":{"from":"2022-01-01T00:00:00","until":"2099-01-01T00:00:00"},"revokable":true,"refunded":false,"cancelable":true,"reactivatable":false,"currency":"usd","created_at":"2022-01-01T00:00:00","updated_at":new Date().toISOString().slice(0,-5),"valid_until":"2099-01-01T00:00:00","auto_renew":true,"price":12.0,"verbose_plan_name":"Termius Pro Monthly","plan_type":"SINGLE","is_expired":false};e.access_objects=[{"period":{"start":"2022-01-01T00:00:00","end":"2099-01-01T00:00:00"},"title":"Pro"}];
```
3. 启动Termius，登录账号
4. 弹出开VIP，关了重启Termius
