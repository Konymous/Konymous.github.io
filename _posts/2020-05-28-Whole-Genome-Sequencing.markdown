---
layout:     post
title:      "个人博客测试页"
subtitle:   "Personal Blog Test Page"
date:       2021-09-23
author:     "Ziyi Zhou"
header-img: "img/bg/2021_9.jpg"
tags: Blog 测试 2021
---

*《格致余论》：“阴阳交媾，胎孕乃凝。”*

* 《温疫论》：“温邪上受，首先犯肺，逆传心包，肺主气属胃，心主血属营，辨营卫气血虽与伤寒同，若论治则与伤寒大异也。”

#### 自我介绍

姓名：雪菲菲
年龄：21岁
出生地：上海
就读学校：上海中医药大学
专业：中医学


```shell
gatk VariantRecalibrator \
	-R ${reference_fa} \
	--resource:hapmap,known=false,training=true,truth=true,prior=15.0 ${hapmap} \
	--resource:omni,known=false,training=true,truth=true,prior=12 ${omni} \
	--resource:1000G,known=false,training=true,truth=false,prior=10.0 ${G1000} \
	--resource:dbsnp,known=true,training=false,truth=false,prior=2.0 ${dbsnp}} \
	-an DP -an FS -an MQ -an QD -an SOR -an MQRankSum -an ReadPosRankSum \
	-mode SNP \
	-tranche 100.0 -tranche 99.9 -tranche 99.0 -tranche 90.0 \
	--max-gaussians 4 \
	-V sample.hc.vcf.gz \
	-O sample.hc.snps.recal.table \
	--tranches-file sample.hc.snps.recal.tranches \
	--rscript-file sample.hc.snps.recal.plots.R
gatk ApplyVQSR \
	-R ${reference_fa} \
	-V sample.hc.vcf.gz \
	--recal-file sample.hc.snps.recal.table \
	--tranches-file sample.hc.snps.recal.tranches \
	-ts-filter-level 99.0 \
	-mode SNP \
	-O sample.hc.snps.vqsr.vcf.gz \
	--create-output-variant-index true
```

