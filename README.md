# scFilterLinux

（1）串联重复序列的屏蔽:
调用TRF（Tandem Repeats Finder）软件[41],在默认参数下对3B染色体序列进行注释与屏蔽,取反提取出未被注释屏蔽区域的序列,然后对序列长度进行筛选(大于等于2000bp)｡由于符合筛选条件的序列数量较多,所以还需要对数据进行分块处理,以便于后续服务器的进度记录与并行运算｡
（2）单拷贝序列的提取:
在每一个数据块中的序列都要进行序列比对｡对于在小麦3B序列上恰好只能比对到自身的序列则可认为是3B单拷贝序列(identity>70%,cover>70%),但大部分情况是在3B范围内会有多次匹配｡这种情况需要剪切掉序列上比对上多次的区域,然后将剪切后的片段汇总后再次用以上方法分析｡在不断迭代的计算过程中,最终得到片段中只能比对上自身的片段并记录所有单拷贝序列的比对信息(起始位点､终止位点､正负链等)｡
（3）数据的合并与验证:
根据各个数据块的执行情况,来实时显示执行进度,同时除去小于2000bp的单拷贝碎片｡将筛选后的单拷贝片段再次与3B染色体进行比对,详细记录比对的结果｡通过对单拷贝序列的提取中得到的比对结果与再次比对信息的检查与比对,即完成了单拷贝序列的验证过程｡
