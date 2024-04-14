# 测试套件

# 测试套件

### 练习1：测试集合

通过简单输入来运行到目前为止编写的所有测试

```
pytest 
```

### 练习2：选项

尝试一些pytest的选项：

```
pytest -v  # verbose output

pytest -lf # re-run failed tests

pytest -x  # stop on first failing test 
```

### 练习3：修复测试

修复`test_suite.py`中的测试

### 练习4：测试选择

只运行一个测试类

```
pytest test_suite.py::TestAverageWordLength 
```

或者单个测试函数：

```
pytest test_suite.py::TestAverageWordLength::test_average_words 
```

你的任务是仅运行**tests/**中测试套件中的函数**test_word_counter.test_simple**。
