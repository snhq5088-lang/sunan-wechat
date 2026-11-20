# 京江后勤集团 · 2026 小雪公众号长图可编辑 PSD

## 文件与打开方式
- `长图-京江后勤集团-小雪节气.psd`：1080 × 7407 px，RGB 8 bit，72 PPI；8,432,365 字节（8.43 MB / 8.04 MiB）。仅制作长图，没有另做单张封面。
- 打开/编辑前安装 `fonts/` 内字体：霞鹜文楷 LXGW WenKai **Light、Regular、Medium**，**Noto Serif CJK SC Regular**、**Cormorant SC Light**、**Inria Sans Light**。内部 PostScript 名已与源字体核对，详见 `fonts/安装清单.md`。
- Noto Serif 为源系统 TTC index 2 的简体中文面，原字形无修改导出为 OTF；其余为原字体文件，附相应 OFL / 许可文件。Noto Sans 虽在源脚本定义，但成稿未使用，不必安装。
- `preview/合成预览-整张.png`：同一图层树的 Pillow 无损整张合成；另附 6 段预览。
- `preview/PSD实读图层合成.png`：psd-tools 从最终 PSD 强制逐层重组的整张预览，不是直接取内嵌合并图。
- `diff/官方-PSD合成-差值.png`：左官方 JPG / 中最终 PSD 实读图层合成 / 右 8 倍绝对差；`差值-8倍.png` 为全尺寸差值图。
- `verification.json`：逐项文案、Type layer、EngineData 与尺寸核验记录。
- `work/`：改写后的旧工具链（build_layers.py、build_psd.js、排版 JSON 及验证脚本）；不是另起设计。

## 做法及图层
优先沿用 `/workspace/xiaoxue-2026/psd/work/` 的 Pillow 栅格缓存 + JSON 字体位置参数 + Node ag-psd Type layer 工作流，并改写为重放本项目 `compose_v2.py` 的真实绘制操作，精确提取字号、字体 PostScript 名、坐标、基线、颜色及字距。没有重设计，也没有从成图抠字。

- 纸色背景：单独纯色像素层，无正文文字。
- 插画：中间冬储手绘、热汤食材、姜枣茶、日常暖居、保温守护、雪枝红柿，共六层。全部使用 `assets_v2/` 原无字素材，执行源脚本原有 blend_to_bg / trim_and_scale；背景与插画均未压入标题、正文或落款。
- 装饰：朱砂红印章「传统节气」、细线、短横杠、圆点、右侧淡蓝竖字及旋转英文水印，均为独立像素层，可移动或隐藏；保留源透明度和层级。
- 01 封面文字至 06 收尾文字：共 **42 个真正 Photoshop Type layer**（TySh / EngineData），包含「小」「雪」、中英文标题、小标题、逐行正文、提问、品牌及日期。每一条视觉行单独可编辑，断行与成图一致；非隐藏文字，也非像素替代文字。
- 封面和结尾以外没有品牌/日期，没有「苏南后勤集团」。
- 英文跟踪字距按源脚本逐字 bbox 步长写入 styleRuns，保留其非整数 FreeType advance 修正。

## 必做核验结果
1. 最终 PSD 经 psd-tools 成功打开，尺寸 **1080 × 7407**，42 个 Type layer 均有非空 EngineData 与 TySh。逐个 Type layer 的文本与排版记录完全一致。
2. ARTICLE_TEXT.txt 的必要文案均通过 Type layer 检索；去掉编辑性栏目标签，按成稿的视觉断行拼接。**原文标题在「小雪到了」后有逗号，已定稿 JPG / compose_v2.py 改为两行且未显示这个逗号，本 PSD 严格遵循成稿，不补逗号。**其余正文、标点与落款逐字保留。
3. 同一图层树 Pillow 合成对源 compose_v2 无损重放的 MAE = **0.000000**。对官方 JPEG 的 MAE = **0.774810**，RMSE = **1.619818**。
4. 从最终 PSD 强制逐层重组对官方 JPEG：**MAE = 0.778405，RMSE = 1.626061，最大通道绝对差 = 33**（0–255 范围）。实读合成对 Pillow 图层预览 MAE = 0.022225，系半透明合成舍入差异。
5. 预览检查未见明显文字错位、重叠或错误断行；极小像素差主要为官方 JPEG 压缩及透明水印混合的舍入。

## 残留限制
- 未在桌面版 Adobe Photoshop 中实机打开测试；已完成最终文件的 PSD 格式解析、EngineData 和像素层树重组核验。Photoshop 第一次编辑文字时会使用自己的排版/抗锯齿引擎重绘，可能与内嵌预览有细微差异；缺字体时将发生字体替换，因此务必先安装附带字体。
- 文字按现有每一视觉行拆为点文字层，能直接改字，但跨行大幅改稿需要自行调整后续行；不会自动整段流式重排。
- 插画为高清像素层，装饰中的印章、水印为独立像素层而非矢量；标题、正文、小标题、落款均是真正 Type layer。
