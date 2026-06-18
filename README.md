# <!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Visualisasi Algoritma Sort & Search</title>

<style>
body{
    font-family:Arial, sans-serif;
    background:#f4f4f4;
    text-align:center;
    padding:50px;
}

.container{
    max-width:700px;
    margin:auto;
}

.card{
    background:white;
    padding:30px;
    border-radius:15px;
    box-shadow:0 0 10px rgba(0,0,0,.1);
}

.btn{
    display:inline-block;
    margin:15px;
    padding:15px 25px;
    text-decoration:none;
    background:#3498db;
    color:white;
    border-radius:10px;
    font-size:18px;
}

.btn:hover{
    background:#2980b9;
}
</style>
</head>

<body>

<div class="container">
    <div class="card">
        <h1>Visualisasi Algoritma Sort & Search</h1>

        <p>
            Tugas Algoritma dan Struktur Data
        </p>

        <a href="sort.html" class="btn">
            Sorting Algorithms
        </a>

        <a href="search.html" class="btn">
            Searching Algorithms
        </a>
    </div>
</div>

</body>
</html>

<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sorting Algorithms</title>

<style>
body{
    font-family:Arial;
    background:#f4f4f4;
    padding:20px;
}

.container{
    max-width:900px;
    margin:auto;
    background:white;
    padding:20px;
    border-radius:15px;
}

input{
    width:100%;
    padding:10px;
    margin:10px 0;
}

button{
    padding:10px 15px;
    margin:5px;
    cursor:pointer;
}

.result{
    margin-top:20px;
    padding:15px;
    background:#eef;
    border-radius:10px;
}
</style>
</head>
<body>

<div class="container">

<h1>Sorting Algorithms</h1>

<p>Masukkan angka dipisahkan koma</p>

<input id="numbers" value="64,34,25,12,22,11,90">

<br>

<button onclick="runBubble()">Bubble Sort</button>
<button onclick="runSelection()">Selection Sort</button>
<button onclick="runInsertion()">Insertion Sort</button>
<button onclick="runQuick()">Quick Sort</button>
<button onclick="runMerge()">Merge Sort</button>
<button onclick="runNative()">JavaScript Sort()</button>

<div class="result" id="result"></div>

</div>

<script>

function getArray(){
    return document
        .getElementById("numbers")
        .value
        .split(",")
        .map(Number);
}

function show(name,data){
    document.getElementById("result").innerHTML=
    `<h3>${name}</h3>
    <p>${data.join(", ")}</p>`;
}

function bubbleSort(arr){
    let n=arr.length;

    for(let i=0;i<n;i++){
        for(let j=0;j<n-i-1;j++){

            if(arr[j]>arr[j+1]){
                [arr[j],arr[j+1]]=
                [arr[j+1],arr[j]];
            }

        }
    }
    return arr;
}

function selectionSort(arr){

    for(let i=0;i<arr.length;i++){

        let min=i;

        for(let j=i+1;j<arr.length;j++){

            if(arr[j]<arr[min]){
                min=j;
            }

        }

        [arr[i],arr[min]]=
        [arr[min],arr[i]];
    }

    return arr;
}

function insertionSort(arr){

    for(let i=1;i<arr.length;i++){

        let key=arr[i];
        let j=i-1;

        while(j>=0 && arr[j]>key){
            arr[j+1]=arr[j];
            j--;
        }

        arr[j+1]=key;
    }

    return arr;
}

function quickSort(arr){

    if(arr.length<=1) return arr;

    let pivot=arr[arr.length-1];

    let left=[];
    let right=[];

    for(let i=0;i<arr.length-1;i++){

        if(arr[i]<pivot)
            left.push(arr[i]);
        else
            right.push(arr[i]);

    }

    return [
        ...quickSort(left),
        pivot,
        ...quickSort(right)
    ];
}

function mergeSort(arr){

    if(arr.length<=1) return arr;

    let mid=Math.floor(arr.length/2);

    let left=mergeSort(arr.slice(0,mid));
    let right=mergeSort(arr.slice(mid));

    return merge(left,right);
}

function merge(left,right){

    let result=[];

    while(left.length && right.length){

        if(left[0]<right[0])
            result.push(left.shift());
        else
            result.push(right.shift());

    }

    return [...result,...left,...right];
}

function runBubble(){
    show("Bubble Sort",
    bubbleSort(getArray()));
}

function runSelection(){
    show("Selection Sort",
    selectionSort(getArray()));
}

function runInsertion(){
    show("Insertion Sort",
    insertionSort(getArray()));
}

function runQuick(){
    show("Quick Sort",
    quickSort(getArray()));
}

function runMerge(){
    show("Merge Sort",
    mergeSort(getArray()));
}

function runNative(){

    let arr=getArray();

    arr.sort((a,b)=>a-b);

    show("JavaScript Array.sort()",arr);
}

</script>

</body>
</html>

<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Searching Algorithms</title>

<style>
body{
    font-family:Arial;
    background:#f4f4f4;
    padding:20px;
}

.container{
    max-width:900px;
    margin:auto;
    background:white;
    padding:20px;
    border-radius:15px;
}

input{
    width:100%;
    padding:10px;
    margin:10px 0;
}

button{
    padding:10px 15px;
    margin:5px;
}

.result{
    margin-top:20px;
    background:#eef;
    padding:15px;
    border-radius:10px;
}
</style>
</head>

<body>

<div class="container">

<h1>Searching Algorithms</h1>

<p>Data (terurut untuk Binary & Interpolation)</p>

<input id="numbers"
value="10,20,30,40,50,60,70,80,90,100">

<input id="target"
placeholder="Masukkan angka yang dicari">

<button onclick="runLinear()">
Linear Search
</button>

<button onclick="runBinary()">
Binary Search
</button>

<button onclick="runInterpolation()">
Interpolation Search
</button>

<button onclick="runHash()">
Hash Lookup
</button>

<div id="result" class="result"></div>

</div>

<script>

function getArray(){
    return document
    .getElementById("numbers")
    .value
    .split(",")
    .map(Number);
}

function getTarget(){
    return Number(
        document.getElementById("target")
        .value
    );
}

function linearSearch(arr,target){

    for(let i=0;i<arr.length;i++){

        if(arr[i]===target){
            return i;
        }

    }

    return -1;
}

function binarySearch(arr,target){

    let left=0;
    let right=arr.length-1;

    while(left<=right){

        let mid=
        Math.floor((left+right)/2);

        if(arr[mid]===target)
            return mid;

        if(arr[mid]<target)
            left=mid+1;
        else
            right=mid-1;
    }

    return -1;
}

function interpolationSearch(arr,target){

    let low=0;
    let high=arr.length-1;

    while(
        low<=high &&
        target>=arr[low] &&
        target<=arr[high]
    ){

        let pos=
        low+
        Math.floor(
            ((high-low)*
            (target-arr[low]))/
            (arr[high]-arr[low])
        );

        if(arr[pos]===target)
            return pos;

        if(arr[pos]<target)
            low=pos+1;
        else
            high=pos-1;
    }

    return -1;
}

function hashLookup(target){

    const data={
        101:"Andi",
        102:"Budi",
        103:"Citra",
        104:"Dewi"
    };

    return data[target] || "Tidak ditemukan";
}

function show(text){

    document.getElementById("result")
    .innerHTML=text;
}

function runLinear(){

    let idx=
    linearSearch(
        getArray(),
        getTarget()
    );

    show(`Index ditemukan: ${idx}`);
}

function runBinary(){

    let idx=
    binarySearch(
        getArray(),
        getTarget()
    );

    show(`Index ditemukan: ${idx}`);
}

function runInterpolation(){

    let idx=
    interpolationSearch(
        getArray(),
        getTarget()
    );

    show(`Index ditemukan: ${idx}`);
}

function runHash(){

    let result=
    hashLookup(getTarget());

    show(`Hasil Hash Lookup: ${result}`);
}

</script>

</body>
</html>