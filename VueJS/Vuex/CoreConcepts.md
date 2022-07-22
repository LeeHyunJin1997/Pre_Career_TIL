# index.js

Vuex의 Core Concepts가 작성되는 곳

![image-20220722114019963](CoreConcepts.assets/image-20220722114019963.png)



# State

Vuex는 single state tree를 사용하며, 여러 컴포넌트에 내부에 있던 특정 state를 중앙에서 관리하게 된다.

이 때, 중앙저장소에 해당하는 것이 State이다.

각 컴포넌트는 State의 정보를 사용하며, State가 변화하면 해당 State를 공유하는 DOM은 알아서 렌더링된다.

모든 데이터를 State에 보관할 필요는 없으며, 여러 컴포넌트에서 공통으로 사용될 데이터 위주로 담는 것이 좋다.
