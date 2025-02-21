---
layout: post
title: "Префикс функция"
author: "kubrikk"
tags: "Строки префикс-функция"
katex: True
---



> Более формально определим префикс функцию $$\pi_{s}(i)$$ от строки $$s$$ в позиции $$i$$:
> 
> $$\pi_{s}(i) = \max_{0 \leq k \leq i}\{ k \ | \ s[0..k-1]=s[i - k + 1..i] \}$$
> 
> * $$\pi_{s}(i)$$ – префикс-функция для строки $$s$$ в позиции $$i$$;
> * $$s[0..k-1]$$ – префикс строки $$s[0..i]$$ длины $$k$$;
> * $$s[i-k+1..i]$$ – суффикс строки $$s[0..i]$$ длины $$k$$.

<!-- Пусть дана строка $s = s_0s_1s_2...s_{n-1}$ длины $n$, где $s_i$ – символ строки на позиции $i$. 
**Префикс-функция** $\pi$ для строки $s$ – это массив  -->

{% highlight cpp  linenos %}
/**
 * Реализация префикс-функции, работающей за O(n^3),
 * где n -- длина строки line. 
 */
vector<int> slow_prefix_function(const string& line) {
    vector<int> prefix_value(line.size(), 0);

    for (int i = 1; i < line.size(); i++) {
        for (int len = 0; len <= i; len++) {
            bool is_matched = true;
            for (int j = 0; j < len; j++) {
                if (line[j] != line[i - len + 1 + j]) { 
                    is_matched &= false; 
                }
            }
            if (is_matched) { prefix_value[i] = len; }
        }
    }

    return prefix_value;
}
{% endhighlight %}

<details>
  <summary>Dropdown Menu</summary>
  - Option 1
  - Option 2
  - Option 3
</details>

```cpp
/**
 * Реализация префикс-функции, работающей за O(n),
 * где n -- длина строки line. 
 */
vector<int> prefix_function(const string& line) {
    vector<int> prefix_value(line.size(), 0);

    for (int i = 1; i < line.size(); i++) {
        int k = prefix_value[i - 1];
        while (k > 0 and line[i] != line[k]) {
            k = prefix_value[k - 1];
        }
        if (line[i] == line[k]) { k += 1; }
        prefix_value[i] = k;
    }

    return prefix_value;
}
```