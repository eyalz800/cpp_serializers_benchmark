# CPP serializers benchmark

### tested libraries
* [bitsery](https://github.com/fraillt/bitsery) 5.2.1
* [boost](https://www.boost.org/) 1.77.0
* [cereal](https://uscilab.github.io/cereal/) 1.3.0
* [flatbuffers](https://google.github.io/flatbuffers/) 2.0.0
* [yas](https://github.com/niXman/yas) 7.1.0
* [protobuf](https://developers.google.com/protocol-buffers/) 3.17.3
* [zpp_bits](https://github.com/eyalz800/zpp_bits) 2.4
* [msgpack](https://github.com/msgpack/msgpack-c) 3.3.0

## GCC 11 (Ubuntu 20.04 x64)

| library     | test case                                                  | bin size | data size | ser time | des time |
| ----------- | ---------------------------------------------------------- | -------- | --------- | -------- | -------- |
| bitsery     | general                                                    | 70904B   | 6913B     | 1426ms   | 1482ms   |
| bitsery     | brief syntax[<sup>1</sup>](#additional-tests-information)  | 70888B   | 6913B     | 1377ms   | 1442ms   |
| bitsery     | compatibility[<sup>2</sup>](#additional-tests-information) | 75192B   | 7113B     | 1253ms   | 1102ms   |
| bitsery     | compression[<sup>3</sup>](#additional-tests-information)   | 70848B   | 4213B     | 1641ms   | 1749ms   |
| bitsery     | fixed buffer[<sup>4</sup>](#additional-tests-information)  | 53648B   | 6913B     | 767ms    | 1262ms   |
| bitsery     | stream[<sup>5</sup>](#additional-tests-information)        | 59568B   | 6913B     | 1375ms   | 5380ms   |
| bitsery     | unsafe read[<sup>6</sup>](#additional-tests-information)   | 66760B   | 6913B     | 1155ms   | 858ms    |
| boost       | general                                                    | 279024B  | 11037B    | 12886ms  | 10635ms  |
| cereal      | general                                                    | 70560B   | 10413B    | 9474ms   | 7748ms   |
| flatbuffers | general                                                    | 70640B   | 14924B    | 7593ms   | 2955ms   |
| handwritten | general[<sup>7</sup>](#additional-tests-information)       | 47936B   | 10413B    | 1296ms   | 1289ms   |
| handwritten | unsafe[<sup>8</sup>](#additional-tests-information)        | 47944B   | 10413B    | 1293ms   | 1065ms   |
| iostream    | general[<sup>9</sup>](#additional-tests-information)       | 53872B   | 8413B     | 10024ms  | 11184ms  |
| msgpack     | general                                                    | 89144B   | 8857B     | 2292ms   | 11809ms  |
| protobuf    | general                                                    | 2077864B | 10018B    | 17587ms  | 18162ms  |
| protobuf    | arena[<sup>10</sup>](#additional-tests-information)        | 2077872B | 10018B    | 8635ms   | 10154ms  |
| yas         | general[<sup>11</sup>](#additional-tests-information)      | 61072B   | 10463B    | 1888ms   | 1444ms   |
| yas         | compression[<sup>12</sup>](#additional-tests-information)  | 65400B   | 7315B     | 2358ms   | 2080ms   |
| yas         | stream[<sup>13</sup>](#additional-tests-information)       | 56184B   | 10463B    | 9446ms   | 9661ms   |
| zpp_bits    | general                                                    | 52192B   | 8413B     | 617ms    | 588ms    |
| zpp_bits    | fixed buffer                                               | 48000B   | 8413B     | 522ms    | 569ms    |

## Clang 12.0.1 (Ubuntu 20.04 x64)

| library     | test case                                                  | bin size | data size | ser time | des time |
| ----------- | ---------------------------------------------------------- | -------- | --------- | -------- | -------- |
| bitsery     | general                                                    | 53728B   | 6913B     | 1878ms   | 1690ms   |
| bitsery     | brief syntax[<sup>1</sup>](#additional-tests-information)  | 55320B   | 6913B     | 2597ms   | 1886ms   |
| bitsery     | compatibility[<sup>2</sup>](#additional-tests-information) | 54360B   | 7113B     | 2084ms   | 1738ms   |
| bitsery     | compression[<sup>3</sup>](#additional-tests-information)   | 54688B   | 4213B     | 4068ms   | 4064ms   |
| bitsery     | fixed buffer[<sup>4</sup>](#additional-tests-information)  | 49248B   | 6913B     | 873ms    | 1715ms   |
| bitsery     | stream[<sup>5</sup>](#additional-tests-information)        | 54776B   | 6913B     | 1859ms   | 5770ms   |
| bitsery     | unsafe read[<sup>6</sup>](#additional-tests-information)   | 49688B   | 6913B     | 1942ms   | 1153ms   |
| boost       | general                                                    | 237008B  | 11037B    | 14174ms  | 12044ms  |
| cereal      | general                                                    | 61480B   | 10413B    | 9292ms   | 8065ms   |
| flatbuffers | general                                                    | 62512B   | 14924B    | 9153ms   | 3347ms   |
| handwritten | general[<sup>7</sup>](#additional-tests-information)       | 43112B   | 10413B    | 1257ms   | 1346ms   |
| handwritten | unsafe[<sup>8</sup>](#additional-tests-information)        | 43120B   | 10413B    | 1240ms   | 1217ms   |
| iostream    | general[<sup>9</sup>](#additional-tests-information)       | 48632B   | 8413B     | 10018ms  | 12039ms  |
| msgpack     | general                                                    | 77384B   | 8857B     | 3431ms   | 14278ms  |
| protobuf    | general                                                    | 2032712B | 10018B    | 16005ms  | 19065ms  |
| protobuf    | arena[<sup>10</sup>](#additional-tests-information)        | 2032760B | 10018B    | 8198ms   | 10492ms  |
| yas         | general[<sup>11</sup>](#additional-tests-information)      | 51000B   | 10463B    | 1496ms   | 1559ms   |
| yas         | compression[<sup>12</sup>](#additional-tests-information)  | 51424B   | 7315B     | 2368ms   | 2613ms   |
| yas         | stream[<sup>13</sup>](#additional-tests-information)       | 54680B   | 10463B    | 9452ms   | 10096ms  |
| zpp_bits    | general                                                    | 47128B   | 8413B     | 666ms    | 661ms    |
| zpp_bits    | fixed buffer                                               | 43056B   | 8413B     | 560ms    | 637ms    |


### Additional tests information

1. deserialization using `brief\_syntax`, similar to `cereal`
2. forward\/backward compatibility enabled for `Monster`
3. all components of Vec3 is compressed in \[-1.0, 1.0\] range with precision 0.01
4. use non-resizable buffer uint8\_t\[150000\] for serialization
5. use stream input\/output adapter, underlying type is std::stringstream
6. on deserialization do not check for errors
7. check buffer size on reading, but writing buffer is preallocated std::array&lt;uint8\_t, 1000000&gt;
8. doesn't check for buffer size when reading, buffer: std::array&lt;uint8\_t, 1000000&gt;
9. use std::stringstream's internal std::string
10. use arena allocator
11. use yas::mem\_&lt;io&gt;stream as buffer
12. with yas::no\_header and yas::compacted
13. using std::stringstream

NOTE: tests for protobuf and flatbuffers is not 100% fair, because huge amount of CPU cycles goes to converting from generated types, to our defined types.

## Why another cpp serializers benchmark

I'm aware that [cpp-serializers](https://github.com/thekvs/cpp-serializers) project already exists, but it's testing set is way too simple and you cannot compile each project to separate executable.

This project contains more realisting data that needs to be serialized.
```cpp
    enum Color : uint8_t {
        Red,
        Green,
        Blue
    };

    struct Vec3 {
        float x;
        float y;
        float z;
    };

    struct Weapon {
        std::string name;
        int16_t damage;
    };

    struct Monster {
        Vec3 pos;
        int16_t mana;
        int16_t hp;
        std::string name;
        std::vector<uint8_t> inventory;
        Color color;
        std::vector<Weapon> weapons;
        Weapon equipped;
        std::vector<Vec3> path;
    };
```

All data is random generated, although seed is hard-coded to get predictable results when running same test multiple times.

All projects implement same interface for serialization and deserialization.
```cpp
struct Buf {
    const uint8_t* ptr;
    size_t bytesCount;
};

class ISerializerTest {
public:
    virtual Buf serialize(const std::vector<MyTypes::Monster>& data) = 0;
    virtual void deserialize(Buf buf, std::vector<MyTypes::Monster>& res) = 0;
    virtual ~ISerializerTest() = default;
};
```

Testing routine consist of few steps:
* data generation step, in which monsters are generated (default 50 monsters)
* warmup step, in which serialization and deserialization is run 5 times, to warmup cpu cache and check if deserialized data equals to original data.
* measurement step, runs serialization and deserialization multiple times (default 300000 samples),
  deserialization happens on same object, to avoid costly allocate operations for new object construction each time.

## Building & testing

1. Build project
    ```bash
    mkdir build && cd build
    cmake ..
    make
    ```
2. Run tests with `ctest -VV` **OR**
3. Generate testing results *(requires nodejs)*
    ```bash
    cd ../tools/
    npm install
    npm start
    ```
