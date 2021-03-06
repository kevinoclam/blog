---
layout: post
title: Possible short name access to ACP backups on Windows servers in MyBB version 1.8.7 [CVE-2016-9418]
---

发现者: 陈瑞琦 

发现日期: 2016-08-28

下载地址: [MyBB](https://mybb.com/versions/)

作者: MyBB

作者通知日期: 2016-08-29

作者联系手段: 

CVE-ID：CVE-2016-9418

**描述:**

b2evolutioe is a content and community management system written in PHP and backed by a MySQL database. It is distributed as free software under the GNU General Public License.
b2evolution originally started as a multi-user multi-blog engine when Fran?ois Planque forked b2evolution from version 0.6.1 of b2/cafelog in 2003.[2] A more widely known fork of b2/cafelog is WordPress. b2evolution is available in web host control panels as a "one click install" web app.[3](Wiki)

**细节:** 
The backup file is public to everyone if the webadmin choose to store it on the server.

But the protect code in 

./inc/tasks/backupdb.php: 

`code`
<pre><code>
$file = MYBB_ADMIN_DIR.'backups/backup_'.date("_Ymd_His_").random_str(16);
<pre><code>

can be bypass in win server.

Using 'backup~1.gz' to get 'backup__20160822_093242_XXKZ8Da9tfv8hm3R.sql.gz'.

Anyone can use a url like 'http://192.168.204.128/mybb/admin/backups/backup~1.gz' to get the backup file.

**PoC:**

'http://192.168.204.128/mybb/admin/backups/backup~1.gz'

**Fix:**

https://github.com/b2evolution/b2evolution/commit/dd975fff7fce81bf12f9c59edb1a99475747c83c