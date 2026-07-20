# ROUTINE-NOTES — 连通性探针

运行时间：2026-07-20（探针运行，自主执行）
执行环境：Claude Code 远程容器，出站 HTTPS 走 agent proxy。

## 摘要（TL;DR）

- **hub.cissychen.com 整站对本环境返回 HTTP 403 Forbidden** —— WebFetch 两个页面全部 403，`curl -sI` 根路径也 403。**无法通过 hub 抓取渲染后的正文。**
- **GitHub 直接 clone 源仓正常** —— `physics` 和 `mental-models` 都 clone 成功。
- **结论方向**：以后这个 routine 要读源页，应当直接 `git clone` GitHub 源仓读取原始文件，而不是走 hub.cissychen.com（当前对本环境不可达/被拒）。

---

## 1. WebFetch — physics/entropy-arrow-day7.html

- URL: `https://hub.cissychen.com/physics/entropy-arrow-day7.html`
- 结果：**失败**
- 完整错误原文：
  ```
  The server returned HTTP 403 Forbidden.
  The response body was not retrieved. If this URL requires authentication,
  use an authenticated tool (e.g. `gh` for GitHub, or an MCP-provided fetch tool) instead of WebFetch.
  ```
- 拿到正文了吗：**没有**。返回的是 403，连页面主体都没取到，无法判断「玻尔兹曼 / S = k log W」是否存在，也无法估算字数。这是服务器层面的拒绝，不是空壳页面。

## 2. WebFetch — mental-models/information-theory-day58.html

- URL: `https://hub.cissychen.com/mental-models/information-theory-day58.html`
- 结果：**失败**
- 完整错误原文：
  ```
  The server returned HTTP 403 Forbidden.
  The response body was not retrieved. If this URL requires authentication,
  use an authenticated tool (e.g. `gh` for GitHub, or an MCP-provided fetch tool) instead of WebFetch.
  ```
- 同样是 403，未取到任何正文。

## 3. Bash — git clone physics

- 命令：`git clone --depth 1 https://github.com/cissy0802/physics /tmp/probe-physics`
- 结果：**成功**（EXIT_CODE=0）
- 耗时：**约 0.66 秒**（0.656s）
- 体积：`du -sh` = **852K**
- 备注：小仓，秒级完成，无任何报错。

## 4. Bash — git clone mental-models

- 命令：`git clone --depth 1 https://github.com/cissy0802/mental-models /tmp/probe-mm`
- 结果：**成功**（EXIT_CODE=0）
- 耗时：**约 51.3 秒**（51.307s）
- 体积：`du -sh` = **1.7G**
- 备注：仓库很大（含大量 TTS mp3），checkout 阶段 958 个文件全部更新完成。**1.7G 对本会话的固定磁盘配额是明显负担**——如果 routine 要反复 clone 这个仓，建议用 sparse-checkout 只拉需要的 html/文本文件，避开 mp3，或用 GitHub MCP `get_file_contents` 按需读单个文件，避免每次 1.7G + 50s 的开销。

## 5. curl — hub 根路径状态码

- 命令：`curl -sI https://hub.cissychen.com/`
- HTTP 状态码：**403 Forbidden**
- 返回头：
  ```
  HTTP/1.1 403 Forbidden
  Content-Length: 36
  ```
- curl 进程退出码 56（recv 阶段连接被重置），但状态行已明确为 403。与第 1、2 项的 WebFetch 403 一致 —— **整站对本环境返回 403**，不是单个页面问题。

---

## 给后续 routine 的建议

1. **不要依赖 hub.cissychen.com 读源页**：当前对本远程环境全站 403（可能是 IP/UA/防火墙/需要认证）。若必须走 hub，需先解决访问授权问题。
2. **优先走 GitHub 源仓**：`git clone` 对 `cissy0802/physics`、`cissy0802/mental-models` 都通。读渲染后正文这条路走不通，但读源文件（html/markdown）没问题。
3. **注意 mental-models 体积**：1.7G / ~51s。反复全量 clone 会吃满磁盘配额，建议 sparse-checkout 或用 GitHub MCP 按需取单文件。
