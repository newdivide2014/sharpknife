+++
lastmod = 2025-07-29T11:16:33+08:00
draft = false
+++

## <span class="org-todo todo TODO">TODO</span> C++ make_shared使用 {#make_shared}


### 概念 {#概念}

`make_shared` 是 `C++11` 引入的模板函数，用于创建并返回一个动态分配对象的 `shared_ptr` ，解决了传统 `shared_ptr` 构造方式存在的内存分配和异常安全问题。


### 与传统方式区别 {#与传统方式区别}

-   传统方式需两次内存分配（对象内存 + 控制块内存）， `make_shared` 通过合并分配减少到一次，提升约 30% 性能。
-   若构造函数抛异常， `make_shared` 保证已分配内存自动释放，避免泄漏；传统方式可能因分配分离导致资源泄露。
-   无需重复类型名称，配合 auto 关键字使代码更简洁。 ‌


### 使用场景 {#使用场景}

‌推荐使用场景‌：自定义类型、复杂对象或性能敏感场景。 ‌
避免使用‌场景：当对象需手动管理生命周期（如依赖外部资源释放函数）时，因 `make_shared` 对象内存延迟释放可能导致问题。


### 释放机制 {#释放机制}

`make_shared` 创建的 `shared_ptr` 对象会在‌最后一个引用该对象的 `shared_ptr` 被销毁时‌释放内存

-   释放条件

当没有任何 `shared_ptr` （强引用）指向由 `make_shared` 创建的对象时，该对象会被自动销毁。若存在 `weak_ptr` （弱引用）指向该对象，则不会立即释放，需等待所有弱引用失效后才会销毁。 ‌

-   释放机制

‌单次内存分配优势‌： `make_shared` 将对象本体与控制块（引用计数等）合并分配内存，仅需一次分配。 ‌
自动管理生命周期‌：当最后一个强引用离开时，对象自动销毁，无需手动调用 `delete` ，避免了内存泄漏风险。 ‌


### 示例 {#示例}

```c++
#include <memory>
std::shared_ptr<T> ptr = std::make_shared<T>(Args&&... args);
```

```c++
#include <iostream>
#include <memory>
using namespace std;

struct A{
  int a;
  char b;
  A(int x)：a(x){ cout << "A constructor" << endl; }
  ~A(){}
};

int main()
{
  //使用auto
  auto sp = make_shared<int>(17);
  //new
  shared_ptr<char> spchar<new char('b')>;

  shared_ptr<A> sptr = make_shared<A>();
  cout << sp->a << endl;
  //数组 c++2及更高版本支持
  shared_ptr<int[]> arr = make_shared<int[]>(10);
  for(int i = 0; i < 10; i++) {
    arr[i] = i+1;
  }
  for(int i = 0; i < 10; i++) {
    cout << arr[i] << " "
  }
  cout << endl;
  //C++11/14 不支持 std::make_shared 创建数组，需使用 std::shared_ptr<int[]>(new int[5])
  return 0;
}
```


### mysql协议分片 {#mysql协议分片}

在实现MySQL协议的分段拼包时，需要处理数据包分片（Packet Fragmentation） 和序列号管理（Sequence ID）。MySQL协议规定：当单个数据包超过16MB-1（0xFFFFFF字节）时，必须拆分成多个分片包传输。以下是实现方案的关键步骤：

每个MySQL数据包包含：
包头（Header）：4字节
前3字节：包体长度（小端字节序）
第4字节：序列号（Sequence ID）
包体（Payload）：实际数据（最大0xFFFFFF字节）

1.  数据包结构

2.  关键细节

序列号循环：
序列号范围是0-255，超过255后回绕到0。
每个新命令的第一个包序列号必须为0。
分片终止条件：
接收端通过当前分片长度 &lt; 0xFFFFFF判断是否为最后一个分片。

大包处理：
发送端：若数据 &gt; 16MB，自动拆分成多个0xFFFFFF分片 + 一个尾部分片。
接收端：持续拼接直到收到长度 &lt; 0xFFFFFF的分片。

错误处理：
序列号不连续：立即中断并报错（可能遭遇中间人攻击或数据损坏）。
包头/包体不完整：抛出IncompletePacketError。

1.  协议示例

假设发送 18MB 数据：
分片1: [包头: 0xFFFFFF + seq=0] + 16MB 数据
分片2: [包头: 0x200000 + seq=1] + 2MB 数据  # 0x200000 = 2MB
注意：最后一个包长度2MB &lt; 0xFFFFFF，触发接收端终止拼接。

1.  优化建议

缓冲区预分配：接收端根据首个包头预估总大小，预分配内存避免多次扩容。
超时机制：为recv()设置超时，防止死等不完整分片。
流量控制：在分片间加入ACK确认（非MySQL标准协议，需自定义扩展）。
通过严格遵循包头中的长度字段和序列号，即可正确处理任意大小的MySQL协议数据包分片。

ProcessPackage(payload, length, direct, this)

1.  操作mysql、oracle数据库，触发分片，抓包结合解析分析报文。
2.  整合代码把之前临时方案改动代码的修改bug部分保留，临时方案剔除。开发mysql缓存报文逻辑。

<!--listend-->

```python
print("hello world!");
```

引擎主动发了fin包
查查为啥


## POPPING日常练习方法 {#popping日常练习方法}


### pop训练： {#pop训练}

-   手臂pop：大臂肱二头肌、三头肌。小臂。
-   大腿pop
-   胸部pop
-   pop强度和速度控制
    -   最大发力爆发 | 弱pop，肌肉微微颤动
    -   pop变速跟音乐（比如同一首歌曲用0.8倍速和原速）


### isolation： {#isolation}

-   头肩胸胯
-   手臂wave
-   body wave
-   touch wave

这里可练的太多了，暂写这么几个吧


### 音乐切分层次处理 {#音乐切分层次处理}

1.  **分层听歌**
    -   只听鼓点（Kick大鼓/Snare军鼓）
    -   聚焦Bass线
    -   捕捉特效音（如电子音效、镲片）

2.  变速切分
    -   突然降速时：放大动作幅度，加入细节控制
    -   突然加速时：简化动作，用高频pop + Step保持节奏


### **重点关注** {#重点关注}

1.  pop的脆感 vs 黏连感
2.  wave的连贯性 vs 断层点
3.  音乐切分是否精准到“碎拍”
