---
layout: post
title:  "[GIT] 깃 블로그에서 수식 사용하기"
date:   2020-12-30T00:14:52-05:00
author: 윤영진
use_math: true
categories: git
tags: git  MathJax 
---
# Jekyll 테마 Github blog에 MathJax를 이용한 수식 입력 가능하게 하기

Jekyll 테마 Github blog에 MathJax를 이용한 수식 입력을 가능하게 하기 위해서는 `_layouts/post.html`에 다음 코드를 삽입해야 한다.

```
<script type="text/x-mathjax-config">
    MathJax.Hub.Config({tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}});
    </script>
    <script type="text/javascript" src="http://cdn.mathjax.org/math...">
</script>
```
![Alt text](/assets/git/math_script.gif "script example")

수식을 이용하기 위해서는 `$[입력할 수식]$` 또는 `$$[입력할 수식]$$` 을 사용해야 한다. 그리고 수식의 문법은 `latex` 문법을 사용한다. `latex` 연습을 하는데 다음 사이트를 참고하면 된다. 

* <https://en.wikibooks.org/wiki/LaTeX/Mathematics> (LaTex docs)
* <https://johngrib.github.io/wiki/mathjax-latex/> (간단한 사용예시)
* <http://detexify.kirelabs.org/classify.html> (모르는 기호를 LaTex 문법으로 맞춰 제안)
* <https://latexbase.com/> (온라인 LaTeX 수식 확인 가능 사이트 -상당히 유용!)

제대로 적용 되었는지 확인하기 위해 다음과 같이 글을 작성해보자.

```
유한체상에 다항식 $f(x) = \sum_{i=0}^{n}a_ix^i$의 미분을 $f'(x)$으로 정의한다.

$$f'(x) = \sum_{i=0}^{n}i\cdot a_ix^{i-1}$$
```

유한체상에 다항식 $f(x) = \sum_{i=0}^{n}a_ix^i$의 미분을 $f'(x)$으로 정의한다.   

$$f'(x) = \sum_{i=0}^{n}i\cdot a_ix^{i-1}$$

--------------------------
# Reference
* <https://seongkyun.github.io/others/2019/01/03/MathJax/>
