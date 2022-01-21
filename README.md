# TIL

✍ 순열과 조합
중복순열 : 요소의 중복을 허용해서 순서를 부여해 조합하는 모든 경우의 수
주어진 요소의 개수보다 많은 요소를 뽑을 수 있다.
[사과,오렌지,레몬] 에서 중복순열이 허용된다면?
[사과,사과,오렌지,레몬]

function forloop() {
let result = [] //결과를 담을 배열을 선언
let lookup = [1,2,3] //코테에서 변수로 안담겨있으면 임의로 추가하자.

for(let i=0;i<lookup.length;i++){
let pick1 = lookup[i]
for(let j=0;j<lookup.length;j++){
let pick2 = lookup[j]
for(let k=0;k<lookup.length;k++){
let pick3 = lookup[k]{
result.push([pick1,pick2,pick3])
}
}
}
return result
}
//좀 더 편리한 정리.
function forloop() {
let result = [] //결과를 담을 배열을 선언
let lookup = [1,2,3] //코테에서 변수로 안담겨있으면 임의로 추가하자.

for(let i=0;i<lookup.length;i++){
for(let j=0;j<lookup.length;j++){
for(let k=0;k<lookup.length;k++){
result.push([lookup[i],lookup[j],lookup[k])
}
}
}
return result
}
순열인 경우는 같은 값이 들어오면 안되므로 조건문을 달아야 한다.

function forloop() {
let result = [] //결과를 담을 배열을 선언
let lookup = [1,2,3] //코테에서 변수로 안담겨있으면 임의로 추가하자.

for(let i=0;i<lookup.length;i++){
for(let j=0;j<lookup.length;j++){
for(let k=0;k<lookup.length;k++){
// || 연산자는 왼쪽에서 오른쪽으로 논리형 판단을 하기 때문에 만약 i===j에서 걸린다면 그 다음 조건들은 무시하고 다시 for문으로 올라간다.
if(i===j || j===k || i===k) continue;
result.push([lookup[i],lookup[j],lookup[k])
}
}
}
return result
}
TIP : continue는 해당 요소만 무시하고 실행, break은 조건문을 통째로 종료시킨다.
조합 : 한번 쓰인 조합의 기준 요소는 제외되는 특징을 가짐

function forloop() {
let result = [] //결과를 담을 배열을 선언
let lookup = [1,2,3] //코테에서 변수로 안담겨있으면 임의로 추가하자.

for(let i=0;i<lookup.length;i++){
//같은 요소를 사용하지 않도록 j=i+1를 사용
for(let j=i+1;j<lookup.length;j++){
result.push(][lookup[i],lookup[j]])
}
}
}
return result
}
❓ 하지만 7개 중 5개를 뽑아서 만든다면 5중 for문을 만들어야 할까?
-> 재귀로 해결하자.

let result = [];
const lookup = [1,2,3]

function recursion(count,bucket){
//재귀 탈출조건
if(count === 0){
result.push(bucket)
return;
}
for(let i=0;i<3;i++){
const pick = lookup[i]
recursion(count-1,bucket.concat(pick)) //push를 사용하는게 아닌가? 할 수 있지만 개발자도구에 push를 하면 최종 배열의 길이를 리턴한다.
//재귀가 끝나기 전까지 for문이 stack에 쌓이고 탈출조건에 도달했을 때 멈춰있던 for문이 돌아가면서 result에 bucket들이 push 된다.
//함수1, 함수2, 함수3, 함수4
//펜으로 써보면서 이해해보자!
}
}
recursion(3,[])
