# 腾讯云监控 / 安全组件卸载 (tencentcloud-agent-uninstaller)

`killqq.sh` —— 腾讯云监控与安全组件一键彻底卸载脚本（全自动执行两遍）。

## 用途

卸载腾讯云 CVM 上预装的监控/安全/管理类 agent，常用于自购或迁移后的机器去除厂商后台组件、减少资源占用与外联。

## 卸载内容

- **TAT Agent**（云助手，远程命令执行）
- **云镜 YunJing**（主机安全）
- **Stargate**、**Barad**（监控组件，先 stop 再 uninstall）
- 删除计划任务 `/etc/cron.d/sgagenttask`
- 清空当前用户的 crontab

为确保彻底，卸载流程会**自动执行两遍**。

## 使用方法

```bash
sudo bash killqq.sh
```

完成后建议重启服务器以彻底生效。

## 依赖与环境

- 系统：腾讯云 Linux（CentOS / Ubuntu / Debian 等）
- 权限：**必须 root**
- 卸载 TAT 会联网下载官方卸载脚本

## ⚠️ 注意事项

- 脚本会执行 `crontab -r`，**清空当前用户的全部定时任务**——如有自定义 cron 任务，请先备份（`crontab -l`）
- 卸载安全组件后主机将失去腾讯云侧的安全防护与监控告警，请自行评估
- 仅适用于腾讯云环境；非腾讯云机器上各组件路径不存在，脚本会安全跳过
