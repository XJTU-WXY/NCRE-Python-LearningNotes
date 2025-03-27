# NCRE 二级 Python 个人学习笔记
本仓库是个人备考 NCRE 二级 Python 的过程中所总结的学习笔记，根据 2025 版考试大纲总结，相比正常的 Python 基础教程更关注那些实际应用中很难注意到但 NCRE 考试非常喜欢当成易错点来出题的“冷知识”。

所有内容均以 IPython Notebook 或 Markdown 的形式呈现。
## 参考资料
- 标学教育b站公共基础知识部分公开网课
- [《Hello 算法》](https://www.hello-algo.com/)
- [Python 3 教程 | 菜鸟教程](https://www.runoob.com/python3/python3-tutorial.html)
- [Python 3.5.10 官方文档](https://docs.python.org/zh-cn/3.5/)
- [fxsjy/jieba](https://github.com/fxsjy/jieba)
- [NumPy 官方文档](https://numpy.org/doc/stable/)
- [Pip 官方文档](https://pip.pypa.io/en/stable/cli/)
- [PyInstaller 官方文档](https://pyinstaller.org/en/stable/)
## 注意事项
- 学习笔记为个人以备考目的总结，存在大量术语用词方面的错误。
- 由于我希望借考试的机会系统重温一遍 Python 基础，为了内容的系统性与完整性，部分内容相比实际考试内容有拔高与深入。
- 由于 NCRE 考试各考点仍在使用极其老旧的 Python 3.5 版本，部分我们在实际应用中习以为常的新版本特性在此考试中均无法使用，请多加注意：
  - 3.5 版本的字典是无序的，其迭代顺序不可预测，在 NCRE 考试中甚至将“字典无序”作为一个考点，而早在 3.6 版本中就已经实现了有序词典，字典默认为保持插入顺序。
  - 3.5 没有 f-strings 字符串格式化，考试只能使用 str.format() 实现字符串格式化。f-strings 是在 3.6 版本引入且在 3.8 版本加强的。
  - 3.5 不能使用 | 来合并两个字典，字典合并运算符是 3.9 版本引入的。
## 共享协议
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)