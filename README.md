## 介绍

一个使用 Cloudflare Pages 创建的 URL 短链生成器

*Demo* : 
[https://d.001315.xyz](https://d.001315.xyz)



### 利用Cloudflare pages部署


1. fork本项目
2. 登录到[Cloudflare](https://dash.cloudflare.com/)控制台.
3. 在帐户主页中，选择`pages`> ` Create a project` > `Connect to Git`
4. 选择你创建的项目存储库，在`Set up builds and deployments`部分中，全部默认即可。
5. 点击`Save and Deploy`，稍等片刻，你的网站就部署好了。
6. 创建D1数据库, 可以命名为` durl ` 也可以自定义.具体参考[这里](https://github.com/shaoyouvip/telegraph-Image/blob/main/docs/manage.md)
7. 执行sql命令创建表（在控制台输入框粘贴下面语句执行即可）

```sql
DROP TABLE IF EXISTS links;
CREATE TABLE IF NOT EXISTS links (
  `id` integer PRIMARY KEY NOT NULL,
  `url` text,
  `slug` text,
  `ua` text,
  `ip` text,
  `status` int,
  `create_time` DATE
);
DROP TABLE IF EXISTS logs;
CREATE TABLE IF NOT EXISTS logs (
  `id` integer PRIMARY KEY NOT NULL,
  `url` text ,
  `slug` text,
  `referer` text,
  `ua` text ,
  `ip` text ,
  `create_time` DATE
);

```
8. 选择部署完成short项目，前往后台依次点击`设置`->`函数`->`D1 数据库绑定`->`编辑绑定`->变量名称填写：`DB` 命名空间 `选择你提前创建好的D1` 数据库绑定

9. 重新部署项目，完成。


### API

#### 短链生成

```bash
# POST /create
curl -X POST -H "Content-Type: application/json" -d '{"url":"https://001315.xyz"}' https://d.001315.xyz/create

# 指定slug
curl -X POST -H "Content-Type: application/json" -d '{"url":"https://001315.xyz","slug":"scxs"}' https://d.001315.xyz/create

```



> response:

```json
{
  "slug": "<slug>",
  "link": "http://d.001315.xyz/<slug>"
}
```

### 鸣谢：
[x-dr](https://github.com/x-dr)
