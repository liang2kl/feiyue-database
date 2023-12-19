# 清华大学飞跃数据库

清华大学飞跃数据库是一个收集并展示清华大学出国申请案例的数据库，旨在帮助同学们更好地了解往届同学的申请情况，为自己的申请提供参考。

数据库中的信息储存于 [SeaTable](https://cloud.seatable.io/dtable/external-links/custom/thu-feiyue/) 中，通过 API 读取并生成网页——这使得对数据进行分类、分析成为可能。网页使用 [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) 生成。我们之后还将支持将数据导出为 LaTex 文档，以 PDF 格式发布。

本文档每 6 小时自动更新一次，并每周使用 Internet Archive 的 Wayback Machine 对文档进行快照。具体细节详见 [Actions 页面](https://github.com/liang2kl/feiyue-database/actions/)。

## 构建文档

### 安装依赖

```bash
pip3 install -r requirements.txt
```

### 构建

目前只支持构建为 MkDocs 网页。访问 API 需要有 SeaTable 的 API Key，目前只有管理员具有访问权限。如果没有 API Key，请参考下文。

使用如下命令构建：

```bash
python3 maker.py --api-key=<seatable-api-key> --frontend=mkdocs --link-resources [--cached]
```

- 使用 `--link-resources` 时，复制静态文档到输出文件夹时将直接创建符号链接，而不是复制文件，这样可以使得 MkDocs 检测到文件的更新，适合在本地开发时打开。
- 使用 `--cache` 时，将会缓存 SeaTable 数据库的数据，而无需使用 API 查询数据库。

如果没有 API Key，可以到 [`publish` Action](https://github.com/liang2kl/feiyue-database/actions/workflows/publish.yml) 中最新的 run 处下载名为 `database-backup` 的 artifact，解压后将 `.cache` 目录复制到项目根目录下，并使用 `--cached` 参数即可。

### 预览

构建完成后，MkDocs 项目将会被输出到 `output` 目录下。使用如下命令启动预览服务器：

```bash
cd output
mkdocs serve
```
