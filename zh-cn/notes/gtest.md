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

- TEST_P

```C++
using ::testing::TestWithParam;
using ::testing::Values;

typedef PrimeTable* CreatePrimeTableFunc();

PrimeTable* CreateOnTheFlyPrimeTable() {
  return new OnTheFlyPrimeTable();
}

template <size_t max_precalculated>
PrimeTable* CreatePreCalculatedPrimeTable() {
  return new PreCalculatedPrimeTable(max_precalculated);
}

class PrimeTableTestSmpl7 : public TestWithParam<CreatePrimeTableFunc*> {
 public:
  ~PrimeTableTestSmpl7() override { delete table_; }
  void SetUp() override { table_ = (*GetParam())(); }
  void TearDown() override {
    delete table_;
    table_ = nullptr;
  }

 protected:
  PrimeTable* table_;
};

TEST_P(PrimeTableTestSmpl7, ReturnsFalseForNonPrimes) {}
TEST_P(PrimeTableTestSmpl7, ReturnsTrueForPrimes) {}
TEST_P(PrimeTableTestSmpl7, CanGetNextPrime) {}
INSTANTIATE_TEST_SUITE_P(OnTheFlyAndPreCalculated, PrimeTableTestSmpl7,
                         Values(&CreateOnTheFlyPrimeTable,
                                &CreatePreCalculatedPrimeTable<1000>));
```

- TEST_P

```C++
using ::testing::TestWithParam;
using ::testing::Bool;
using ::testing::Values;
using ::testing::Combine;

class PrimeTableTest : public TestWithParam< ::std::tuple<bool, int> > {
 protected:
  void SetUp() override {
    bool force_on_the_fly;
    int max_precalculated;
    std::tie(force_on_the_fly, max_precalculated) = GetParam();
    table_ = new HybridPrimeTable(force_on_the_fly, max_precalculated);
  }
  void TearDown() override {
    delete table_;
    table_ = nullptr;
  }
  HybridPrimeTable* table_;
};

TEST_P(PrimeTableTest, ReturnsFalseForNonPrimes) {}
TEST_P(PrimeTableTest, ReturnsTrueForPrimes) {}
TEST_P(PrimeTableTest, CanGetNextPrime) {}
INSTANTIATE_TEST_SUITE_P(MeaningfulTestParameters, PrimeTableTest,
                         Combine(Bool(), Values(1, 10)));
```

- 内存泄漏检查

```c++
using ::testing::EmptyTestEventListener;
using ::testing::InitGoogleTest;
using ::testing::Test;
using ::testing::TestEventListeners;
using ::testing::TestInfo;
using ::testing::TestPartResult;
using ::testing::UnitTest;

namespace {
class Water {
 public:
  void* operator new(size_t allocation_size) {
    allocated_++;
    return malloc(allocation_size);
  }
  void operator delete(void* block, size_t /* allocation_size */) {
    allocated_--;
    free(block);
  }
  static int allocated() { return allocated_; }
 private:
  static int allocated_;
};
int Water::allocated_ = 0;

class LeakChecker : public EmptyTestEventListener {
 private:
  void OnTestStart(const TestInfo& /* test_info */) override {
    initially_allocated_ = Water::allocated();
  }
  void OnTestEnd(const TestInfo& /* test_info */) override {
    int difference = Water::allocated() - initially_allocated_;
    EXPECT_LE(difference, 0) << "Leaked " << difference << " unit(s) of Water!";
  }
  int initially_allocated_;
};
TEST(ListenersTest, DoesNotLeak) {
  Water* water = new Water;
  delete water;
}
TEST(ListenersTest, LeaksWater) {
  Water* water = new Water;
  EXPECT_TRUE(water != nullptr);
}
}

int main(int argc, char **argv) {
  InitGoogleTest(&argc, argv);

  // 检查内存泄漏
  bool check_for_leaks = false;
  if (argc > 1 && strcmp(argv[1], "--check_for_leaks") == 0 )
    check_for_leaks = true;
  else
    printf("%s\n", "Run this program with --check_for_leaks to enable "
           "custom leak checking in the tests.");
  if (check_for_leaks) {
    TestEventListeners& listeners = UnitTest::GetInstance()->listeners();
    listeners.Append(new LeakChecker);
  }

  return RUN_ALL_TESTS();
}
```

- gcov

> [qingl812/gtest-cmake-lcov-example](https://github.com/qingl812/)

> 参考资料 https://qiita.com/imasaaki/items/0021d1ef14660184f396gtest-cmake-lcov-example

```
# gcov
set(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} --coverage")
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} --coverage")
```