# jsw 群发言活跃度排行榜 · 加密页

本仓库只存放**口令加密后**的报告页 `index.html`，明文报告不在仓库内。

- 线上地址：https://guxiao7538.github.io/jsw-activity-ranking/
- 打开后输入群内公布的口令即可解锁完整报告

## 关于加密

- AES-256-GCM 认证加密，密钥由 PBKDF2-HMAC-SHA256（60 万次迭代）从口令派生
- 密文被改动会直接解密失败，因此页面里渲染的内容一定是原始报告
- 解密在浏览器本地完成，口令不上传任何服务器

## 为什么这么做

报告含群成员昵称、地域、性别等个人信息，不适合明文放公网。
公网只放密文，口令走微信群单独发布，群友拿到链接 + 口令即可查看。

## 更新报告

在分析工作区的 `jsw-activity/` 下重新生成报告后：

```bash
JSW_REPORT_PASSWORD='口令' python3 encrypt_report.py \
  --input out/<新报告>.html --output out/<新报告>.locked.html --unwrap-srcdoc
cp out/<新报告>.locked.html pages/index.html
cd pages && git add -A && git commit -m "update report" && git push
```
