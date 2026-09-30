# qq-email

QQ 邮箱收发邮件 Agent Skill —— IMAP 收信 + SMTP 发信，凭据全部走环境变量，零硬编码。

## 功能

| 脚本 | 作用 |
| --- | --- |
| `scripts/send.js` | 发送 QQ 邮件（收件人 / 主题 / 正文，支持 stdin） |
| `scripts/receive.js` | 收取最近 N 条 / N 天邮件，输出主题、发件人、日期、UID、正文摘要 |
| `scripts/get-body.js` | 按 UID 获取指定邮件的完整正文（纯文本） |

## 配置

```bash
export QQ_EMAIL_ACCOUNT="your_email@qq.com"    # QQ 邮箱完整地址
export QQ_EMAIL_AUTH_CODE="16位授权码"           # 非 QQ 登录密码！
```

授权码获取：QQ 邮箱网页版 → 设置 → 账户 → 开启 IMAP/SMTP 服务 → 短信验证生成。

## 服务器

- IMAP: `imap.qq.com:993` (SSL)
- SMTP: `smtp.qq.com:465` (SSL)

## 安装

```bash
npm install    # 依赖：nodemailer / imap / mailparser
```

## 使用

```bash
# 发信
node scripts/send.js "recipient@example.com" "主题" "正文内容"

# 收最近 10 条（默认）/ N 条 / N 天
node scripts/receive.js
node scripts/receive.js --limit 20
node scripts/receive.js --days 7

# 按 UID 取完整正文
node scripts/get-body.js --uid 12345
```

## 来源

上游：https://github.com/shadowcz007/skills （`skills/qq-email` 目录，MIT 风格开源 skill 集）
本仓库为独立 skill 切片，已实测收发闭环可用。
