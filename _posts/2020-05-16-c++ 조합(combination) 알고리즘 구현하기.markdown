---
layout: post
title:  "c++ 조합(combination) 알고리즘 구현하기"
date:   2020-05-16 14:36:41 +0900
categories: 
---
알고리즘 풀이에 있어서 전체 n개의 원소중에서 r개 의 원소를 선택해 직접 해봐야 하는 문제들이 많다.
이럴떄 기계적으로 그 코드를 생각 해내면 많은 시간 단축이 있을 것 같아. 코드를 적어 두려한다..


{% highlight c %}
void combination(int start, int count, vector<pair<int,int>> picked) {
    // k select
    if (count == k) {
		//somthing
    }

    for (int i = start; i < chickens.size(); ++i) {
        picked.push_back(chickens[i]);
        combination(i+1,count+1, picked);
        picked.pop_back();
    }

}

void Solve() {
    vector<pair<int,int>> temp;
    combination(0,0, temp);
}
{% endhighlight %}


