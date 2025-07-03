<template>
<p> Item no.1 : {{ item1 }}</p>
<p> Item no.2 : {{ filterItems }}</p>
<p> Item no.3 : {{ item3 }}</p>
<p> Item no.4 : {{ item4 }}</p>
<p> Item no.5 : {{ accountName }}</p>
<p> Item no.6 : {{ over18 }}</p>
<p> Item no.7 : {{ item7 }}</p>
<p> Item no.9 : {{ item9 }}</p>
<p> Item no.10 : {{ item10 }}</p>
<p> Item no.11 : {{ item11 }}</p>
<p> Item no.12 : {{ item12 }}</p>
<p> Item no.13 : {{ item13 }}</p>
<p> Item no.14 : {{ item14 }}</p>
<p> Item no.15 : {{ item15 }}</p>
<p> Item no.16 : {{ item16 }}</p>
<p> Item no.17 : {{ item17 }}</p>
<p> Item no.18 : {{ item18 }}</p>
<p> Item no.19 : {{ item19 }}</p>
<p> Item no.20 : {{ item20 }}</p>
<p> Item no.21 : {{ item21 }}</p>
</template>
<script setup>

const numbers = [1,2,3,4,5]
//item1
const doubleFunc =(num) =>{
     return num*2
}
const itemMap = numbers.map(doubleFunc)
const item1 = itemMap.join(',')

//item2

const allItems = [true, false, null, 0, '', NaN, undefined, 'Left', 1, 'Right'];


const checkItems = (item) => {
        return item || item === 0 || item === false;
}

const filterItems = allItems.filter (checkItems)

//item3
const users = [
    {id:1, username: 'alice'},
    {id:2, username: 'bob'},
    {id:3, username: 'cathy'},
    {id:4, username: 'derek'},
    {id:5, username: 'elias'},
]

const mappedItem = users.map (user => user.username)
const item3 = mappedItem.join(',')

//item4
const reduceAdd = (total, int) =>{
    return total + int;
}
const item4 = numbers.reduce(reduceAdd)

//item5

const account = [
    {name:'John', role: 'user'},
    {name:'Jane', role: 'admin'},
    {name:'Zhy', role: 'staff'},
    {name:'Vlad', role: 'member'},
    {name:'Arki', role: 'staff'},
    {name:'Rod', role: 'user'},
]

const checkAdmin = (acc) => {
    return acc.role === 'admin'   
}

const item5 = account.find(checkAdmin)
const accountName = item5.name


//item6

const people = [    
    {name:'John', age: 27, gender: 'male'},
    {name:'Jane', age: 2, gender: 'female'},
    {name:'Zhy', age: 8, gender: 'female'},
    {name:'Vlad', age: 28, gender: 'male'},
    {name:'Arki', age: 5, gender: 'male'},
    {name:'Rod', age: 6, gender: 'male'},
]

const checkAge = (pips) => {
    return pips.age > 18
}

const item6 = people.some(checkAge)
let over18 =[]

if (item6){
    
    const newPips = people
     .filter(member => member.age>18)
     .map (({name,age}) => ({name, age}))
     over18 = newPips
}

else {
    over18 = 'No members above 18'
}

people.forEach(element =>{
    delete element.gender
})

let item21=people

//item7
const products = [    
    {name:'Pen', quantity: 15},
    {name:'Pencil', quantity:  25},
    {name:'Paper', quantity:  0},
    {name:'Notebook', quantity: 90},
    {name:'Book', quantity:  25},
    {name:'Crayons', quantity: 17},
]

const checkQnty = (prod) => {
    return prod.quantity > 0
}
const item7 = products.every(checkQnty)

//item 9
const letters = ['a', 'b', 'b', 'c' , 'a', 'd']
const item9 = letters.reduce ((reduced, item)=>{
    if (item !=='c'){
        reduced[item] = (reduced[item] || 0) + 1 
    }
    return reduced
}, {})


//item10
const arr2D = [[1,2],[2,4],[5,6]]
const item10 = arr2D.flat()
//item11

const duplicates = [18,12,12,18,27,34,5,27]
const item11 = duplicates.filter((numbers, index) => duplicates.indexOf(numbers) === index)
//item12

const salad = ['carrot', 'lettuce', 'mayo', 'tomatoes', 'corns']
const largeSalad = (ingredients) => {
    return ingredients.charAt(0).toUpperCase() + ingredients.slice(1)
}
const item12 = salad.map(largeSalad)

//item13

const item13 = {
    firstName : 'Aira'
}

const oldName = item13.firstName
item13.firstName = 'Joshua'
item13.first_name = oldName

// delete item13.firstName;



//14

const object = {a:1, b:2, c:3}
const item14 = Object.entries(object)

//15
const arr = [['a', 1], ['b', 2], ['c', 3]]
const item15 = Object.fromEntries(arr)

//16

const a = {x:1}
const b = {y:2}
const item16 = {...a, ...b}


//17
const original = {
  name: "Ai",
  details: {
    age: 22,
    address: { city: "Batangas", zip: 4224 }
  }
};

const item17 = structuredClone(original);
//18
// const mainObj = {a: 1, b: 2, c: 3}
// const item18 = Object.fromEntries(
//     Object.entries(mainObj).map (([key,value])=> [value,key])
// )

const mainObj = {a: 1, b: 2, c: 3};
let switchItem = {};

Object.keys(mainObj).forEach((key) => {
    const value = mainObj[key]
   switchItem[value] = key
})
 const item18 = switchItem
//19

const obj = { d: 1, e: 2, f: 3 };
const { e, ...item19 } = obj;


//20

const item20 = [    
    {name:'John', age: 15},
    {name:'Jane', age: 2},
    {name:'Zhy', age: 18},
    {name:'Vlad', age: 8},
    {name:'Arki', age: 12},
    {name:'Rod', age: 26},
] 

item20.sort((x, y) => x.age - y.age)

</script>

<style scoped></style>
