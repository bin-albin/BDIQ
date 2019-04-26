# 大数据场景和算法类\[1-10\]

试题一：有 10 个文件，每个文件 1G，每个文件的每一行存放的都是用户的 query，每个文件的query 都可能重复。要求你按照 query 的频度排序

解题方案一：

顺序读取 10 个文件，按照 hash\(query\)%10 的结果将 query 写入到另外 10 个文件（记为）中。这样新生成的文件每个的大小大约也 1G（假设 hash 函数是随机的）。 找一台内存在 2G 左右的机器，依次对用 hash\_map\(query, query\_count\)来统计每个query 出现的次数。利用快速/堆/归并排序按照出现次数进行排序。将排序好的 query 和对应的 query\_cout 输出到文件中。这样得到了 10 个排好序的文件（记为）。 对这 10 个文件进行归并排序（内排序与外排序相结合）

解题方案二：


