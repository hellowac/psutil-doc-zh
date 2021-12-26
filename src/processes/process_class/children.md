# 子进程

**Process.children(recursive=False)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.children) <a name="Process.children" ></a>

将此进程的子进程作为 Process 实例列表返回。如果 ***recursive*** 为 `True` ，则返回所有父子后代。假设A为一个进程的伪代码示例：

```python
  A ─┐
    │
    ├─ B (child) ─┐
    │             └─ X (grandchild) ─┐
    │                                └─ Y (great grandchild)
    ├─ C (child)
    └─ D (child)

>>> p.children()
B, C, D
>>> p.children(recursive=True)
B, X, Y, C, D
```

**注释**: 在上面的例子中，如果进程 X 消失，进程 Y 也不会被返回，因为对进程 A 的引用丢失了。 这个[单元测试][unite-test-children]很好地总结了这个概念。 另请参阅如何[终止进程树](#kill-process-tree)和[终止子进程](#kill-children-process)。

[unite-test-children]: https://github.com/giampaolo/psutil/blob/65a52341b55faaab41f68ebc4ed31f18f0929754/psutil/tests/test_process.py#L1064-L1075 "父子进程单元测试"