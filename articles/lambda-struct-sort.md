---
title: "【C++】ラムダ式を使い倒す：for_eachとsortを使用して構造体を持つ物体間を最短距離で移動する"
emoji: "🌊"
type: "tech"
topics: [coo,lambda, "algorithm", "struct", "vector"]
published: false
---

C++言語の`class`は、自身に対して関数を定義して、自身の変数を参照したりできます.
動かない、

が共通して持っている値を総当り的に探してみました。`any_of`はC++11以降対応のアルゴリズムです。`a`,`b`が共通して持っている値を総当り的に探してみました。`any_of`はC++11以降対応のアルゴリズムです。


```cpp
#include <iostream>
struct Object{
    std::string name;
    int     hp;
    double  position_x;
    double  position_y;

    // 情報を出力する関数
    void
    print(){
        std::cout << "name:" << name << std::endl;
        std::cout << "hp:"  << hp << std::endl;
        std::cout << "position_x:"   << position_x << std::endl;
        std::cout << "position_y:"   << position_y << std::endl;
    }
};

int main() {

Object homu = { "tsubo", 3, 2.0, 2.4 };
homu.print();

}

#include <iostream>
#include <vector>
#include <algorithm>

int main() {
  vector< int > a = { 1, 2, 3, 4, 5 };
  vector< int > b = { 5, 6, 7, 8, 9 };
  vector< int > match_numbers;

  for_each( a.begin(), a.end(), [ &match_numbers, &b ] ( const int &a_element ){

    bool is_match = any_of( b.begin(), b.end(), [ &a_element ] ( const int &b_element ){
      return ( a_element == b_element );
    });

    if ( is_match ) {
      match_numbers.push_back(a_element);
    }
  });

  for_each( match_numbers.begin(), match_numbers.end(), [] ( const int &match_number ){  
    cout <<  match_number << endl;
  });

```

```cpp:実行結果
5
```