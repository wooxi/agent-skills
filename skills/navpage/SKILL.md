---
name: navpage
description: 管理 navpage 导航站——新增/修改/删除链接与分组、更换图标、调整站点的时钟/天气/壁纸/搜索引擎等外观设置。当用户要求改动一个 navpage 实例上的任何内容时使用。
---

# navpage 导航站

- 站点地址：`http://192.168.100.4:8788`
- 鉴权：当前未启用 token，内网可直接调用写接口。若暴露到公网，请设置 `NAVPAGE_TOKEN` 并让 agent 带上 `X-Navpage-Token`。
- 数据模型：`groups`（分组，有 sort 顺序）→ `links`（链接，属于某个 group）。链接字段：`name`、`url`（内网地址）、`url_out`（外网地址，可空）、`icon`（图标，可空）、`description`（可空，界面不展示）。

## 能力

1. 增删改链接（名称、内网/外网地址、图标、所属分组）
2. 增删改分组，调整分组与组内链接的顺序
3. 给链接挑图标：列出候选 → 预览 → 选中（会落地成本地文件）
4. 修改站点设置（搜索引擎、时钟、天气城市、壁纸、界面风格…）
5. 备份数据库

## 接口

所有接口以 `http://192.168.100.4:8788` 为前缀，JSON 收发。

| 方法 | 路径 | 说明 |
| --- | --- | --- |
| GET | `/api/health` | 存活检查，返回链接/分组数量 |
| GET | `/api/links` | 全部链接；`?groupId=1` 只取该组 |
| POST | `/api/links` | 新增：`{name, url, groupId, url_out?, icon?, description?}` |
| PUT | `/api/links/:id` | 局部更新，只传要改的字段 |
| DELETE | `/api/links/:id` | 删除，返回被删行（可据此恢复） |
| PUT | `/api/links/order` | 组内排序：`{groupId, ids:[3,1,2]}` |
| GET | `/api/groups` | 分组列表 |
| POST | `/api/groups` | 新增分组：`{name}` |
| PUT | `/api/groups/:id` | 改名：`{name}` |
| DELETE | `/api/groups/:id` | 删除；组内还有链接时返回 409 |
| PUT | `/api/groups/order` | 分组排序：`{ids:[2,1,3]}` |
| GET | `/api/settings` | 全部设置（永远是完整键集） |
| PUT | `/api/settings` | 批量写：`{key: value}`，任一键非法则整批 400 |
| GET | `/api/settings/schema` | 设置项的键、默认值、取值范围 |
| GET | `/api/icon-candidates?u=<url>` | 候选图标来源列表 |
| GET | `/api/favicon?u=<host>&src=<key>` | 图标代理（`src=auto` 用缓存） |
| POST | `/api/upload` | 上传图片，multipart 字段名 `file`，返回 `{url}` |
| GET | `/api/backup` | 下载 SQLite 快照 |

## 三条常用配方

### 1. 新增一条链接（图标自动抓）

```bash
# 先看看有哪些分组
curl -s http://192.168.100.4:8788/api/groups

# 新增（icon 留空 = 服务端按域名自动抓 favicon）
curl -s -X POST http://192.168.100.4:8788/api/links \
  -H 'Content-Type: application/json' \
  -d '{"name":"Jellyfin","url":"http://192.168.1.10:8096","groupId":2}'
```

### 2. 给已有链接换图标

```bash
# 1) 列出候选来源（site / apple / google / iconhorse / faviconim / duckduckgo）
curl -s 'http://192.168.100.4:8788/api/icon-candidates?u=https://www.bilibili.com'

# 2) 把选中的那张下载下来，再上传成本地图标
curl -s 'http://192.168.100.4:8788/api/favicon?src=iconhorse&u=bilibili.com' -o /tmp/icon.png
curl -s -X POST http://192.168.100.4:8788/api/upload -F 'file=@/tmp/icon.png'
# → {"url":"/api/uploads/1712...png"}

# 3) 写回链接
curl -s -X PUT http://192.168.100.4:8788/api/links/12 \
  -H 'Content-Type: application/json' \
  -d '{"icon":"/api/uploads/1712...png"}'
```

也可以直接把 `icon` 设成公网图片地址，或 `text:🏠` 这种文字图标。

### 3. 批量整理

```bash
# 全部链接导出成 JSON，本地改完再逐条 PUT
curl -s http://192.168.100.4:8788/api/links > links.json
```

排序接口要求 `ids` 完整覆盖该组；跨组或非法 id 会被服务端拒绝（400），不会出现"部分成功"。

## 规则

- 地址必须是 `http://` 或 `https://`；没写协议的会被当成 host 自动补全。内网地址可以直接填 `192.168.1.10:8096`。
- 写接口默认有频率限制（约 60 次/分钟），批量操作请顺序执行，不要并发轰炸。
- 图标：优先 `apple`（高清）或 `iconhorse`；`site` 最真实但常常只有 32px。内网主机只有 `site` 与 `apple` 两个来源可用。
- 改设置前先 `GET /api/settings` 看现有值，只 PUT 要改的键。
- 删除分组前先确认组内没有链接（否则 409）。

## 出错时

- `400` 带 `error` 字段：请求体不合法，按提示改。
- `409`：分组非空。
- `413`：请求体超过 2MB（上传接口 10MB）。
- `429`：触发限流，等几十秒再试。
