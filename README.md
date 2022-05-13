## crontab
cron is the name of the tool, crontab is generally the file that lists the jobs that cron will be executing, and those jobs are, surprise surprise, cronjobs.
* 沒有cronjobs這個程式或指令，指的是cron jobs
參考: https://stackoverflow.com/questions/21615673/difference-between-cron-crontab-and-cronjob


* 注意`crontab -e`編輯與`crontab -r`刪除，e與r位置相當接近，且`crontab -r`是不會出現確認視窗的
  可以考慮直接用vi編輯避免誤刪


### 不自動寄信

crontab 只要執行有輸出文字的話,預設就會將輸出的文字寄出，若要設定不自動寄信
可以將輸出導到 `/dev/null`
```
* * * * * curl -kXGET 'https://v178.qrgo.com.tw/module/blackcat/cronjob' > /dev/null 2>&1
```
其中 `> /dev/null 2>&1` 表示將輸出丟棄
* 1 表示標準輸出 stdout (standard output)
* 2 表示錯誤輸出 stderr (standard error output)
* & 表示等同的意思，&1 表示等同於1，2>&1 表示2的輸出重定向等同於1

這篇解釋得相當清楚  
參考: https://www.itread01.com/content/1550134446.html



## yum repo
yum設定檔放在`/etc/yum.conf`
最下面一行
```
# PUT YOUR REPOS HERE OR IN separate files named file.repo
# in /etc/yum.repos.d
```
說明repo detail也可設定在`/etc/yum.repos.d`裡，
但副檔名一定要repo才起作用

yum.repos.d裡的每個設定檔都會起作用

查看enabled的軟體庫
```bash
yum repolist enabled
```

查看package使用了哪個repository安裝
```bash
repoquery -i [package-name]
```

參考:
https://www.slashroot.in/yum-repository-and-package-management-complete-tutorial
https://serverfault.com/questions/62026/how-to-know-from-which-yum-repository-a-package-has-been-installed
