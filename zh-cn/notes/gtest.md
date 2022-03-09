# EXPECT

- EXPECT_EQ 相等
- EXPECT_NE 不相等
- EXPECT_LT 小于
- EXPECT_LE 小于等于
- EXPECT_GT 大于
- EXPECT_GE 大于等于

- EXPECT_FALSE
- EXPECT_TRUE

- TEST_F

```C++
// 在这个示例中，我们希望确保每个测试都在 0-5 秒。
// 如果测试需要更长的时间来运行，我们认为它是失败。
class QuickTest : public testing::Test {
protected:
	void SetUp() override { start_time_ = time(nullptr); }
	void TearDown() override {
		const time_t end_time = time(nullptr);
		EXPECT_TRUE(end_time - start_time_ <= 5) << "The test took too long.";
	}
	time_t start_time_;
};
```

- TYPED_TEST_SUITE_P

```C++
template <class T>
class PrimeTableTest2 : public PrimeTableTest<T> {};
TYPED_TEST_SUITE_P(PrimeTableTest2);

TYPED_TEST_P(PrimeTableTest2, ReturnsFalseForNonPrimes) {}
TYPED_TEST_P(PrimeTableTest2, ReturnsTrueForPrimes) {}
TYPED_TEST_P(PrimeTableTest2, CanGetNextPrime) {}

REGISTER_TYPED_TEST_SUITE_P(
    PrimeTableTest2,
    ReturnsFalseForNonPrimes, ReturnsTrueForPrimes, CanGetNextPrime);

typedef Types<OnTheFlyPrimeTable, PreCalculatedPrimeTable>
    PrimeTableImplementations;
INSTANTIATE_TYPED_TEST_SUITE_P(OnTheFlyAndPreCalculated,    // Instance name
                               PrimeTableTest2,             // Test case name
                               PrimeTableImplementations);  // Type list
```

- gcov

> [qingl812/gtest-cmake-lcov-example](https://github.com/qingl812/)

> 参考资料 https://qiita.com/imasaaki/items/0021d1ef14660184f396gtest-cmake-lcov-example

```
# gcov
set(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} --coverage")
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} --coverage")
```