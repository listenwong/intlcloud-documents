## 概述

您可以通过 [日志服务控制台](https://console.cloud.tencent.com/cls)，将数据按照 JSON 格式投递到对象存储 COS，下面将为您详细介绍如何创建 JSON 格式日志投递任务。


## 前提条件

1. 开通日志服务，创建日志集与日志主题，并成功采集到日志数据。
2. 开通腾讯云对象存储服务（COS），并且在待投递日志主题的地域已创建存储桶，详细配置您可参阅 [创建存储桶](https://intl.cloud.tencent.com/document/product/436/13309) 文档。
3. 确保当前操作账号拥有配置投递的权限。

## 操作步骤

1. 登录 [日志服务控制台](https://console.cloud.tencent.com/cls)。
2. 在左侧导航栏中，单击【日志集管理】。
3. 单击需要设置投递任务的日志集 ID/名称，进入日志集详情页。
![](https://main.qcloudimg.com/raw/637f191003d50812d117bd32b84b4b0d.png)
4. 找到需要投递的日志主题，在其操作栏中，单击【管理配置】>【投递对象存储配置】，进入投递配置页面。
![](https://main.qcloudimg.com/raw/f2ae55d386797b52d2fca31eae783df1.png)
5. 单击【添加投递配置】，进入**投递至 COS** 配置页面，依次填写配置信息。
   ![img](https://main.qcloudimg.com/raw/c588bcb6e91bb9849003532968edac44.png)

**配置项说明如下：**

<table>
   <tr>
      <th>配置项</th>
      <th>解释说明</th>
      <th>规则</th>
      <th>是否必填</th>
   </tr>
   <tr>
      <td nowrap="nowrap">投递任务名称</td>
      <td>配置投递任务的名称。</td>
      <td nowrap="nowrap">字母、数字、_和-</td>
      <td>必填</td>
   </tr>
   <tr>
      <td nowrap="nowrap">COS 存储桶</td>
      <td>与当前日志主题同地域的存储桶作为投递目标存储桶。</td>
      <td>列表选择</td>
      <td>必填</td>
   </tr>
   <tr>
      <td>目录前缀</td>
      <td>日志服务支持自定义目录前缀，日志文件会投递至对象存储 Bucket 的该目录下。目前默认是直接放在存储桶下，文件路径为 <code>{COS 存储桶}{目录前缀}{分区格式}_{random}_{index}.{type}</code>，其中<code>{random}_{index}</code>是一个随机数。</td>
      <td>非/开头</td>
      <td>可选</td>
   </tr>
   <tr>
      <td nowrap="nowrap">分区格式</td>
      <td>将投递任务创建时间按照 strftime 的语法自动生成目录 ，其中斜线/表示一级 COS 目录。</td>
      <td>strftime 格式</td>
      <td>必填</td>
   </tr>
   <tr>
      <td nowrap="nowrap">投递文件大小</td>
      <td>指定在该投递时间间隔中未压缩的投递文件上限，意味着在该时间间隔中，日志文件最大将为您设置的值，超过该上限，将被分成多个日志文件，上限支持100MB - 10000MB。</td>
      <td nowrap="nowrap">100 - 10000，单位：MB</td>
      <td>必填</td>
   </tr>
   <tr>
      <td>投递间隔时间</td>
      <td>指定投递的时间间隔，支持60s - 3600s。假设您设置投递时间间隔为5分钟，那么意味着您的日志数据将每5分钟产生一个日志文件，每隔一段时间（半小时内），多个日志文件会一起投递至您的存储桶。</td>
      <td nowrap="nowrap">60 - 3600，单位：s</td>
      <td>必填</td>
   </tr>
</table>

上表中的分区格式请按照 [strftime 格式](http://man7.org/linux/man-pages/man3/strptime.3.html) 要求填写，不同的分区格式会影响投递到对象存储的文件路径。 以下举例说明分区格式的用法，例如投递至 bucket_test 存储桶，目录前缀为`logset/`，投递时间 2018/7/31 17:14，则对应的投递文件路径如下：

| 存储桶名称  | 目录前缀 | 分区格式   | cos 文件路径                                     |
| ----------- | -------- | ---------- | ------------------------------------------------ |
| bucket_test | logset/  | %Y/%m/%d   | bucket_test:logset/2018/7/31_{random}_{index}    |
| bucket_test | logset/  | %Y%m%d/%H  | bucket_test:logset/20180731/14_{random}_{index}  |
| bucket_test | logset/  | %Y%m%d/log | bucket_test:logset/20180731/log_{random}_{index} |

6. 单击【下一步】，进入高级配置，选择投递格式为 json，依次填写相关配置参数。
   ![img](https://main.qcloudimg.com/raw/3711401cfd70d3f583bb82dae1970331.png)

**配置项说明如下：**

<table>
   <tr>
      <th>配置项</th>
      <th>解释说明</th>
      <th>规则</th>
      <th>是否必填</th>
   </tr>
   <tr>
      <td nowrap="nowrap">压缩投递</td>
      <td>是否对日志文件进行压缩后投递，在投递时的未压缩文件大小上限为10GB 。目前支持的压缩方式有 gzip 和 lzop。</td>
      <td nowrap="nowrap">开/关</td>
      <td nowrap="nowrap">必填</td>
   </tr>
</table>

**高级选项（可选）**
日志投递还支持根据日志内容进行过滤投递，您可以打开高级选项进行配置。
您可以指定一个 key，对该键值所对应的值进行正则提取，并设定提取出的部分需要匹配的值。只有当日志数据匹配您的配置后，该日志可以投递。没有匹配的日志不进行投递。
如下图所示，指定 action 字段，该字段为 write 时，日志进行投递。投递过滤规则最多支持5条。
![img](https://main.qcloudimg.com/raw/fa774d5a865c2129f707465c55e416c7.png)
7. 单击【确定】，即可看到投递状态已开启。
![img](https://main.qcloudimg.com/raw/f3b59a24524ba51f6bc6c14f9fdfbdba.png)
