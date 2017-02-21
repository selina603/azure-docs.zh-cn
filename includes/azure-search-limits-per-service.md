存储受磁盘空间限制，或者受索引或文档的*最大数目*的硬性限制，具体取决于哪一个限制先实施。

| 资源 | 免费 | 基本 | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| 服务级别协议 (SLA) |否 <sup>1</sup> |是 |是 |是 |是 |是 |
| 每个分区的存储 |50 MB |2 GB |25 GB |100 GB |200 GB |200 GB |
| 每个服务的分区数 |不适用 |1 |12 |12 |12 |3 <sup>2</sup> |
| 分区大小 |不适用 |2 GB |25 GB |100 GB |200 GB |200 GB |
| 副本 |不适用 |3 |12 |12 |12 |12 |
| 最大索引数 |3 |5 |50 |200 |200 |每个分区 1000，或者每个服务 3000 |
| 最大索引器数 |3 |5 |50 |200 |200 |无索引器支持 |
| 最大数据源数 |3 |5 |50 |200 |200 |无索引器支持 |
| 最大文档数 |10,000 |1 百万 |每个分区 1500 万，或者每个服务 1 亿 8 千万 |每个分区 6 千万，或者每个服务 7 亿 2 千万 |每个分区 1 亿 2 千万，或者每个服务 14 亿 |每个索引 1 百万，或者每个分区 2 亿 |
| 每秒估计的查询数 (QPS) |不适用 |每个副本大约&3; 个 |每个副本大约&15; 个 |每个副本大约&60; 个 |每个副本大约&60; 个 |每个副本大于&60; 个 |

<sup>1</sup> 免费版和预览版 SKU 不带服务级别协议 (SLA)。 SKU 公开发布以后，就会强制实施 SLA。

<sup>2</sup> S3 HD 的硬性限制为 3 个分区，低于 S3 的分区限制。 施加的分区限制较低是因为 S3 HD 的索引计数要高得多。 由于计算资源（存储和处理）和内容（索引和文档）都存在服务限制，因此会先达到内容限制。


<!--HONumber=Feb17_HO2-->

