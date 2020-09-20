主题设置

## 示例

```yaml
layout: # 列出对应布局在layout文件夹中的文件名
  post: post.html
  page: page.html
  index: index.html
  tags_index: tags_index.html
  categories_index: categories_index.html

  # post,page,index,tags_index,categories_index为必填项
  # 下面可以自定义布局

  tags_cloud: tags_cloud.html
  links: links.html
  "404": 404.html

defaut_front: # 要在每篇 文章/分页 的frontmatter中默认补充的信息
  comment: True

extra_render: # 扩展渲染页面
- 
  layout: tags_cloud # 指定布局(比如上面自定义的tags_cloud)
  addr: tags/ # 输出到生成文件夹中的地址
  title: 标签云 # 标题
-
  layout: "404"
  addr: 404.html
  title: 404 Page Not found
```