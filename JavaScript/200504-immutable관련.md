immutable js 
push -> 원본 바꾼다.
concat -> 원본 바꾸지 않는다.

var map1 = Immutable.Map({a:1, b:2 c:3});
var map2 = map1.set('b', 50);
map1.get('b'); //2
map2.get('b'); //50