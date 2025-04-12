用于管理 SSH 密钥的程序。

## 1 ssh-agent 无法启动

有时启动 ssh-agent 会报错

![有时启动 ssh-agent 会报错](./../../../images/Issues%20of%20ssh-agent/%E6%9C%89%E6%97%B6%E5%90%AF%E5%8A%A8%20ssh-agent%20%E4%BC%9A%E6%8A%A5%E9%94%99.png)

可能是禁用了 SSH 服务

![可能是禁用了 SSH 服务](./../../../images/Issues%20of%20ssh-agent/%E5%8F%AF%E8%83%BD%E6%98%AF%E7%A6%81%E7%94%A8%E4%BA%86%20SSH%20%E6%9C%8D%E5%8A%A1.png)

按 `Win+R` 运行 `services.msc` 即可查看服务

![运行服务](./../../../images/Issues%20of%20ssh-agent/%E8%BF%90%E8%A1%8C%E6%9C%8D%E5%8A%A1.png)
